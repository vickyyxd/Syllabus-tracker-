<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Syllabus Tracker</title>
<style>
  @import url('https://fonts.googleapis.com/css2?family=Poppins:wght@400;600&display=swap');

  body {
    font-family: 'Poppins', Arial, sans-serif;
    padding: 30px 15px;
    background: linear-gradient(135deg, #667eea, #764ba2);
    color: #fff;
    min-height: 100vh;
  }

  h1 {
    text-align: center;
    font-weight: 600;
    margin-bottom: 40px;
    text-shadow: 0 2px 5px rgba(0,0,0,0.3);
  }

  .subject {
    background: rgba(255, 255, 255, 0.1);
    padding: 25px 30px;
    margin-bottom: 25px;
    border-radius: 15px;
    box-shadow: 0 8px 20px rgba(0, 0, 0, 0.15);
    transition: background 0.3s ease, box-shadow 0.3s ease;
  }

  .subject:hover {
    background: rgba(255, 255, 255, 0.15);
    box-shadow: 0 12px 30px rgba(0, 0, 0, 0.3);
  }

  .subject h2 {
    font-weight: 600;
    margin-bottom: 18px;
    letter-spacing: 1px;
  }

  .unit {
    margin: 12px 0;
    display: flex;
    align-items: center;
    cursor: pointer;
    user-select: none;
  }

  /* Custom checkbox styles */
  .unit input[type="checkbox"] {
    appearance: none;
    -webkit-appearance: none;
    width: 22px;
    height: 22px;
    border-radius: 6px;
    border: 2px solid #8e44ad;
    margin-right: 15px;
    cursor: pointer;
    position: relative;
    transition: background-color 0.3s ease, border-color 0.3s ease;
  }

  .unit input[type="checkbox"]:checked {
    background: #9b59b6;
    border-color: #9b59b6;
  }

  .unit input[type="checkbox"]:checked::after {
    content: '✔';
    color: white;
    font-size: 16px;
    position: absolute;
    top: 1px;
    left: 4px;
  }

  .progress-bar {
    background: rgba(255, 255, 255, 0.25);
    border-radius: 25px;
    overflow: hidden;
    margin: 20px 0 0;
    height: 24px;
    box-shadow: inset 0 2px 5px rgba(0,0,0,0.15);
  }

  .progress-bar-fill {
    height: 100%;
    background: linear-gradient(90deg, #8e44ad, #9b59b6);
    width: 0%;
    border-radius: 25px;
    transition: width 0.5s ease;
  }

  button {
    display: block;
    margin: 40px auto 0;
    padding: 14px 50px;
    background: linear-gradient(135deg, #8e44ad, #9b59b6);
    color: #fff;
    font-weight: 600;
    font-size: 18px;
    border: none;
    border-radius: 35px;
    box-shadow: 0 5px 15px rgba(155, 89, 182, 0.5);
    cursor: pointer;
    transition: box-shadow 0.3s ease, background 0.3s ease;
  }

  button:hover {
    background: linear-gradient(135deg, #9b59b6, #8e44ad);
    box-shadow: 0 8px 25px rgba(155, 89, 182, 0.75);
  }

  /* Responsive tweaks */
  @media (max-width: 600px) {
    body {
      padding: 20px 10px;
    }

    .subject {
      padding: 20px;
    }

    button {
      width: 100%;
      padding: 15px 0;
      font-size: 20px;
    }
  }
</style>

</head>

<body>
    <h1>Syllabus Tracker<br>
    Time:-10.00 AM To 12.30 PM</h1>

    <div class="subject" data-subject="DSBDA">
        <h2>DSBDA [Monday
26-05]
</h2>
        <div class="unit"><input type="checkbox" /> Unit 3: Big Data Analytics Life Cycle</div>
        <div class="unit"><input type="checkbox" /> Unit 4: Predictive Big Data Analytics with Python</div>
        <div class="unit"><input type="checkbox" /> Unit 5: Big Data Analytics and Model Evaluation</div>
        <div class="unit"><input type="checkbox" /> Unit 6: Data Visualization and Hadoop</div>
        <div class="progress-bar">
            <div class="progress-bar-fill"></div>
        </div>
    </div>

    <div class="subject" data-subject="WT">
        <h2>WT [Wednesday
28-05]</h2>
        <div class="unit"><input type="checkbox" /> Unit 3: Java Servlets and XML</div>
        <div class="unit"><input type="checkbox" /> Unit 4: JSP and Web Services</div>
        <div class="unit"><input type="checkbox" /> Unit 5: Server Side Scripting Languages</div>
        <div class="unit"><input type="checkbox" /> Unit 6: Ruby and Rails</div>
        <div class="progress-bar">
            <div class="progress-bar-fill"></div>
        </div>
    </div>

    <div class="subject" data-subject="AI">
        <h2>AI [Friday
30-05]</h2>
        <div class="unit"><input type="checkbox" /> Unit 3: Adversarial Search and Games</div>
        <div class="unit"><input type="checkbox" /> Unit 4: Knowledge</div>
        <div class="unit"><input type="checkbox" /> Unit 5: Reasoning</div>
        <div class="unit"><input type="checkbox" /> Unit 6: Planning</div>
        <div class="progress-bar">
            <div class="progress-bar-fill"></div>
        </div>
    </div>

    <div class="subject" data-subject="CC">
        <h2>CC [Monday
02-06]</h2>
        <div class="unit"><input type="checkbox" /> Unit 3: Virtualization in Cloud Computing</div>
        <div class="unit"><input type="checkbox" /> Unit 4: Cloud Platforms and Cloud Applications</div>
        <div class="unit"><input type="checkbox" /> Unit 5: Security in Cloud Computing</div>
        <div class="unit"><input type="checkbox" /> Unit 6: Advanced Techniques in Cloud Computing</div>
        <div class="progress-bar">
            <div class="progress-bar-fill"></div>
        </div>
    </div>
    <button id="saveButton">Save Progress</button>

    <script type="module">
        import { initializeApp } from "https://www.gstatic.com/firebasejs/10.11.1/firebase-app.js";
        import { getFirestore, doc, setDoc, getDoc } from "https://www.gstatic.com/firebasejs/10.11.1/firebase-firestore.js";

        const firebaseConfig = {
            apiKey: "AIzaSyASuEsQB4qs57gpnqol9IN0Vzl7mlTepUo",
            authDomain: "syllabus-tracker-e8ba0.firebaseapp.com",
            projectId: "syllabus-tracker-e8ba0",
            storageBucket: "syllabus-tracker-e8ba0.appspot.com",
            messagingSenderId: "898810875690",
            appId: "1:898810875690:web:1058fa575311eb1d4dd853",
            measurementId: "G-ZT2F2SVFHZ"
        };

        const app = initializeApp(firebaseConfig);
        const db = getFirestore(app);
        const userDoc = doc(db, "users", "demoUser");

        function updateProgress(subjectEl) {
            const checkboxes = subjectEl.querySelectorAll("input[type='checkbox']");
            const fill = subjectEl.querySelector(".progress-bar-fill");
            let checkedCount = 0;
            checkboxes.forEach(cb => { if (cb.checked) checkedCount++; });
            const percent = (checkedCount / checkboxes.length) * 100;
            fill.style.width = percent + "%";
        }

        function collectProgress() {
            const data = {};
            document.querySelectorAll(".subject").forEach(sub => {
                const name = sub.dataset.subject;
                const checkboxes = sub.querySelectorAll("input[type='checkbox']");
                data[name] = [];
                checkboxes.forEach(cb => data[name].push(cb.checked));
            });
            return data;
        }

        function applyProgress(data) {
            document.querySelectorAll(".subject").forEach(sub => {
                const name = sub.dataset.subject;
                const checkboxes = sub.querySelectorAll("input[type='checkbox']");
                if (data[name]) {
                    data[name].forEach((val, idx) => {
                        if (checkboxes[idx]) checkboxes[idx].checked = val;
                    });
                }
                updateProgress(sub);
            });
        }

        async function saveProgressToFirebase() {
            const data = collectProgress();
            await setDoc(userDoc, data);
            alert("Saved successfully!");
        }

        async function loadProgressFromFirebase() {
            const snap = await getDoc(userDoc);
            if (snap.exists()) {
                applyProgress(snap.data());
            }
        }

        document.querySelectorAll("input[type='checkbox']").forEach(cb => {
            cb.addEventListener("change", () => {
                const sub = cb.closest(".subject");
                updateProgress(sub);
            });
        });

        document.getElementById("saveButton").addEventListener("click", () => {
            saveProgressToFirebase().catch(err => alert("Error saving: " + err));
        });

        loadProgressFromFirebase().catch(console.error);
    </script>
</body>

</html>
