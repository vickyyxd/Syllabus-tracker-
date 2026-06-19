# 📅 Daily Productivity Planner

A modern Flask-based Productivity Planner that helps users manage daily tasks, track progress, monitor productivity, and organize schedules efficiently. The application includes task management, completion tracking, category organization, statistics, and customizable wallpapers.

## ✨ Features

* ✅ Create, edit, and delete tasks
* 📂 Organize tasks by categories
* 🎯 Mark tasks as completed for specific dates
* 📊 Productivity statistics dashboard
* 🔥 Track completion streaks
* 🎨 Customizable wallpapers

## 🛠️ Technologies Used

### Backend

* Python
* Flask
* Flask-CORS

### Database

* JSON File Storage (`data.json`)

### Data Handling

* JSON

## 📁 Project Structure

```
project/
│
├── app.py
├── data.json
├── templates/
│   └── index.html
│
├── static/
│   ├── css/
│   ├── js/
│   └── images/
│
└── README.md
```

## 📌 Categories

The planner includes predefined categories:

* Study
* Gym
* Art of Living
* Coding
* IIT Madras
* Other

Each category has its own color theme for better visualization.

## 🚀 Installation

### 1. Clone Repository

```bash
git clone https://github.com/yourusername/daily-productivity-planner.git
cd daily-productivity-planner
```

### 2. Create Virtual Environment

```bash
python -m venv venv
```

### 3. Activate Environment

Windows:

```bash
venv\Scripts\activate
```

Mac/Linux:

```bash
source venv/bin/activate
```

### 4. Install Dependencies

```bash
pip install flask flask-cors
```

### 5. Run Application

```bash
python app.py
```

The application will start at:

```text
http://localhost:5050
```

Returns:

* Total Tasks
* Completed Today
* Streak
* Category Distribution

### Wallpaper

| Method | Endpoint         |
| ------ | ---------------- |
| GET    | `/api/wallpaper` |
| POST   | `/api/wallpaper` |

### Categories

| Method | Endpoint          |
| ------ | ----------------- |
| GET    | `/api/categories` |

## 📊 Productivity Tracking

The application tracks:

* Daily completed tasks
* Category-wise productivity
* Current productivity streak
* Total active tasks

## 🎨 Customization

Users can:

* Change wallpapers
* Use custom wallpapers
* Assign custom colors to tasks
* Create personalized schedules

## 🔮 Future Improvements

* User Authentication
* Cloud Database Support
* Dark Mode
* Notifications & Reminders
* Weekly & Monthly Analytics
* Calendar View
* Export Data Feature

## 🤝 Contributing

Contributions, issues, and feature requests are welcome.

1. Fork the repository
2. Create a feature branch
3. Commit your changes
4. Push to your branch
5. Open a Pull Request

## 📜 License

This project is open-source and available under the MIT License.

## 👨‍💻 Author

**Vicky Kumar**

Built to help students, coders, gym enthusiasts, and productivity lovers manage their daily routines efficiently.

