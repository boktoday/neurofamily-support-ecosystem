# TOOLS.md — Artifacts Generator 🎨

## Template: Visual Schedule (Morning/Evening)

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>[CHILD NAME]'s Morning Routine</title>
    <style>
        /* Add your styles here */
        :root { --primary: #4A90D9; --success: #5CB85C; --bg: #F5F7FA; }
        body { font-family: system-ui, sans-serif; background: var(--bg); padding: 20px; }
        .schedule { max-width: 600px; margin: 0 auto; }
        .step { background: white; padding: 15px; margin: 10px 0; border-radius: 12px; 
                display: flex; align-items: center; gap: 15px; box-shadow: 0 2px 8px rgba(0,0,0,0.1); }
        .step.completed { opacity: 0.6; }
        .step-number { background: var(--primary); color: white; width: 32px; height: 32px; 
                       border-radius: 50%; display: flex; align-items: center; justify-content: center; font-weight: bold; }
        .step.completed .step-number { background: var(--success); }
        .step-content { flex: 1; }
        .step-title { font-weight: bold; font-size: 1.1em; }
        .step-time { color: #666; font-size: 0.9em; }
        .timer-btn { background: var(--primary); color: white; border: none; padding: 8px 16px; 
                     border-radius: 8px; cursor: pointer; }
        .timer { font-size: 1.5em; font-weight: bold; color: var(--primary); }
    </style>
</head>
<body>
    <h1>🌅 [CHILD NAME]'s Morning Routine</h1>
    <div class="schedule">
        <!-- Step 1 -->
        <div class="step" id="step1">
            <div class="step-number">1</div>
            <div class="step-content">
                <div class="step-title">Wake up & Stretch</div>
                <div class="step-time">7:00 AM</div>
            </div>
            <button class="timer-btn" onclick="startTimer(1, 5)">⏱️ 5 min</button>
        </div>
        <!-- Add more steps -->
    </div>
    <script>
        // Timer logic
        function startTimer(stepId, minutes) {
            let timeLeft = minutes * 60;
            const timer = document.querySelector(`#step${stepId} .timer`);
            if (!timer) return;
            
            const interval = setInterval(() => {
                timeLeft--;
                const m = Math.floor(timeLeft / 60);
                const s = timeLeft % 60;
                timer.textContent = `${m}:${s.toString().padStart(2, '0')}`;
                
                if (timeLeft <= 0) {
                    clearInterval(interval);
                    // Play sound or notify
                }
            }, 1000);
        }
    </script>
</body>
</html>
```

---

## Template: Mood/Emotion Tracker

```html
<!-- Quick mood check-in -->
<div class="mood-tracker">
    <h3>How are you feeling?</h3>
    <div class="moods">
        <button class="mood-btn" onclick="logMood('great')">😄 Great</button>
        <button class="mood-btn" onclick="logMood('good')">🙂 Good</button>
        <button class="mood-btn" onclick="logMood('okay')">😐 Okay</button>
        <button class="mood-btn" onclick="logMood('low')">😔 Low</button>
        <button class="mood-btn" onclick="logMood('awful')">😢 Awful</button>
    </div>
    <textarea id="moodNotes" placeholder="What's happening? (optional)"></textarea>
    <button onclick="saveMood()">Save</button>
</div>
```

---

## Template: IEP Goal Tracker

```html
<!-- IEP Goal Card -->
<div class="goal-card">
    <h4>📚 Goal: Reading Comprehension</h4>
    <div class="progress-bar">
        <div class="progress" style="width: 65%">65%</div>
    </div>
    <div class="goal-meta">
        <span>📅 Review: March 15, 2026</span>
        <span>👤 Support: Mrs. Smith</span>
    </div>
    <div class="milestones">
        <label><input type="checkbox"> Identify main idea</label>
        <label><input type="checkbox"> Answer WH questions</label>
        <label><input type="checkbox"> Summarize passage</label>
    </div>
</div>
```

---

## Template: Data Log Entry

```javascript
// localStorage data structure for trackers
const logEntry = {
    id: Date.now(),
    date: "2026-03-03",
    time: "07:30",
    type: "meltdown", // mood | meltdown | food | sleep | sensory | medication
    value: 8, // severity 1-10
    trigger: "transition to school", // what triggered it
    notes: "Long transition, noisy environment",
    whatHelped: "deep pressure, quiet room",
    duration: "25 minutes"
};

// Save to localStorage
function saveEntry(entry) {
    const data = JSON.parse(localStorage.getItem('trackerData') || '[]');
    data.push(entry);
    localStorage.setItem('trackerData', JSON.stringify(data));
}
```

---

## CSS Variables for Theming

```css
:root {
    /* Calming palette (good for anxiety/regulation) */
    --calm-primary: #6B9AC4;
    --calm-secondary: #97C1A9;
    --calm-bg: #F0F4F8;
    --calm-text: #2D3748;
    
    /* Energetic palette (good for motivation/rewards) */
    --energy-primary: #FF6B6B;
    --energy-secondary: #4ECDC4;
    --energy-bg: #FFF9F0;
    
    /* Child-friendly (bright, fun) */
    --kid-primary: #FFD93D;
    --kid-secondary: #6BCB77;
    --kid-accent: #4D96FF;
    
    /* High contrast (accessibility) */
    --contrast-bg: #FFFFFF;
    --contrast-text: #000000;
}
```

---

## Sample Artifacts to Build

### 1. Morning Routine Dashboard
- Visual timeline
- Timer per step
- Celebration on completion
- Parent notes section

### 2. Meltdown Log
- Date/time picker
- Trigger dropdown (customizable)
- Severity slider
- Duration timer
- "What helped" text field
- Weekly/monthly charts

### 3. Food Diary
- Meal slots (breakfast, lunch, dinner, snacks)
- Food items (text + photo upload)
- Safe/New/Refused tags
- Notes on context
- Weekly pie chart of food groups

### 4. Sleep Tracker
- Bedtime and wake time
- Sleep quality (1-5 stars)
- Night wake count
- Dreams/nightmares notes
- Weekly sleep average

### 5. Sensory Dashboard
- 8 senses checkboxes
- Regulation rating before/after activities
- Overwhelm alerts
- Triggers identified
- Calming strategies used

### 6. IEP Timeline
- Goals as cards
- Progress bars
- Review dates
- Accommodations list
- Milestone achievements

### 7. Reward Chart
- Star/point accumulation
- Custom rewards list
- Streak counter
- Level/badge system
- Celebration animations

### 8. First-Then Board
- "First" task (with image)
- "Then" reward (with image)
- Timer option
- Completion celebration

### 9. Choice Board
- 2x2 or 3x3 grid
- Images/icons for each choice
- TTS on tap
- Categories: food, activity, place

### 10. Social Script Reader
- Situation cards
- Script text
- TTS playback
- Visual cues
- "What to do" steps

---

## Accessibility Checklist

- [ ] Colour contrast ratio ≥ 4.5:1
- [ ] Touch targets ≥ 44x44px
- [ ] No flashing/blinking > 3 per second
- [ ] Keyboard navigation for all actions
- [ ] Alt text for images
- [ ] Clear, simple language
- [ ] Consistent layout
- [ ] Error messages are helpful

---

## Technical Notes

- Use `<template>` for reusable components
- Use `localStorage` for persistence
- Use `URL.createObjectURL` for file downloads
- Use `navigator.clipboard` for copy features
- Use `speechSynthesis` API for TTS
- Mobile-first responsive design
- Progressive enhancement (works without JS, better with it)
