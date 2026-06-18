from flask import Flask, render_template, jsonify, request
from flask_cors import CORS
import json
import os
from datetime import datetime, date

app = Flask(__name__)
CORS(app)

DATA_FILE = "data.json"

DEFAULT_DATA = {
    "tasks": [
        {"id": 1, "category": "Study", "title": "Mathematics", "start": "08:00", "end": "10:00", "color": "#6366f1", "done_dates": [], "archived": False},
        {"id": 2, "category": "Gym", "title": "Workout Session", "start": "06:00", "end": "07:30", "color": "#f43f5e", "done_dates": [], "archived": False},
        {"id": 3, "category": "Art of Living", "title": "Volunteer Work", "start": "17:00", "end": "19:00", "color": "#10b981", "done_dates": [], "archived": False},
        {"id": 4, "category": "Coding", "title": "DSA Practice", "start": "20:00", "end": "22:00", "color": "#f59e0b", "done_dates": [], "archived": False},
        {"id": 5, "category": "IIT Madras", "title": "BS Data Science Lecture", "start": "14:00", "end": "16:00", "color": "#8b5cf6", "done_dates": [], "archived": False},
        {"id": 6, "category": "Coding", "title": "Python Programming", "start": "10:30", "end": "12:00", "color": "#06b6d4", "done_dates": [], "archived": False},
        {"id": 7, "category": "Study", "title": "Physics Revision", "start": "16:00", "end": "17:00", "color": "#ec4899", "done_dates": [], "archived": False},
    ],
    "wallpaper": "gradient_1",
    "custom_wallpaper": None,
    "next_id": 8
}

CATEGORIES = ["Study", "Gym", "Art of Living", "Coding", "IIT Madras", "Other"]
CATEGORY_COLORS = {
    "Study": "#6366f1",
    "Gym": "#f43f5e",
    "Art of Living": "#10b981",
    "Coding": "#f59e0b",
    "IIT Madras": "#8b5cf6",
    "Other": "#64748b"
}

def load_data():
    if os.path.exists(DATA_FILE):
        with open(DATA_FILE, "r") as f:
            return json.load(f)
    return DEFAULT_DATA.copy()

def save_data(data):
    with open(DATA_FILE, "w") as f:
        json.dump(data, f, indent=2)

@app.route("/")
def index():
    return render_template("index.html")

@app.route("/api/tasks", methods=["GET"])
def get_tasks():
    data = load_data()
    today = str(date.today())
    tasks = [t for t in data["tasks"] if not t.get("archived", False)]
    return jsonify({"tasks": tasks, "today": today})

@app.route("/api/tasks", methods=["POST"])
def add_task():
    data = load_data()
    body = request.json
    new_task = {
        "id": data.get("next_id", 100),
        "category": body.get("category", "Other"),
        "title": body.get("title", "New Task"),
        "start": body.get("start", "09:00"),
        "end": body.get("end", "10:00"),
        "color": body.get("color", CATEGORY_COLORS.get(body.get("category", "Other"), "#64748b")),
        "done_dates": [],
        "archived": False
    }
    data["tasks"].append(new_task)
    data["next_id"] = data.get("next_id", 100) + 1
    save_data(data)
    return jsonify({"task": new_task, "today": str(date.today())})

@app.route("/api/tasks/<int:task_id>", methods=["PUT"])
def update_task(task_id):
    data = load_data()
    body = request.json
    for t in data["tasks"]:
        if t["id"] == task_id:
            t["title"] = body.get("title", t["title"])
            t["category"] = body.get("category", t["category"])
            t["start"] = body.get("start", t["start"])
            t["end"] = body.get("end", t["end"])
            t["color"] = body.get("color", t["color"])
            save_data(data)
            return jsonify({"task": t, "today": str(date.today())})
    return jsonify({"error": "Not found"}), 404

@app.route("/api/tasks/<int:task_id>", methods=["DELETE"])
def delete_task(task_id):
    data = load_data()
    data["tasks"] = [t for t in data["tasks"] if t["id"] != task_id]
    save_data(data)
    return jsonify({"success": True})

@app.route("/api/tasks/<int:task_id>/toggle", methods=["POST"])
def toggle_task(task_id):
    data = load_data()
    today = str(date.today())
    body = request.json or {}
    target_date = body.get("date", today)
    for t in data["tasks"]:
        if t["id"] == task_id:
            if target_date in t["done_dates"]:
                t["done_dates"].remove(target_date)
                done = False
            else:
                t["done_dates"].append(target_date)
                done = True
            save_data(data)
            return jsonify({"done": done, "task": t})
    return jsonify({"error": "Not found"}), 404

@app.route("/api/stats", methods=["GET"])
def get_stats():
    data = load_data()
    today = str(date.today())
    tasks = [t for t in data["tasks"] if not t.get("archived", False)]
    total = len(tasks)
    done_today = sum(1 for t in tasks if today in t.get("done_dates", []))
    streak = 0
    for t in tasks:
        if t.get("done_dates"):
            streak = max(streak, len(t["done_dates"]))
    cats = {}
    for t in tasks:
        c = t["category"]
        cats[c] = cats.get(c, 0) + 1
    return jsonify({"total": total, "done_today": done_today, "streak": streak, "categories": cats})

@app.route("/api/wallpaper", methods=["GET"])
def get_wallpaper():
    data = load_data()
    return jsonify({"wallpaper": data.get("wallpaper", "gradient_1"), "custom": data.get("custom_wallpaper")})

@app.route("/api/wallpaper", methods=["POST"])
def set_wallpaper():
    data = load_data()
    body = request.json
    data["wallpaper"] = body.get("wallpaper", "gradient_1")
    data["custom_wallpaper"] = body.get("custom_wallpaper", None)
    save_data(data)
    return jsonify({"success": True})

@app.route("/api/categories", methods=["GET"])
def get_categories():
    return jsonify({"categories": CATEGORIES, "colors": CATEGORY_COLORS})

if __name__ == "__main__":
    app.run(debug=True, port=5050)
