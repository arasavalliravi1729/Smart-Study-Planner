this is my entire code for this project.
# Smart-Study-Planner
A web-based study planner for students to manage tasks, track progress, and get reminders with a clean, interactive dashboard.
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Smart Study Planner</title>
<link rel="stylesheet" href="style.css">
</head>
<body>

<header class="header">
  <h1>Smart Study Planner</h1>
  <p class="header-quote">“Success is the sum of small efforts repeated day in and day out.” – Robert Collier</p>
</header>

<main class="main-container"> 

  <!-- Add/Edit Task Panel -->
  <section class="panel task-panel">
    <h2>Add / Edit Task</h2>
    <form id="task-form">
      <input type="hidden" id="task-id">

      <label>Title
        <input type="text" id="title" placeholder="E.g. Revise Thermodynamics" required>
      </label>

      <label>Description
        <textarea id="description" rows="3" placeholder="Optional details..."></textarea>
      </label>

      <label>Due Date & Time
        <input type="datetime-local" id="dueDate">
      </label>

      <label>Priority
        <select id="priority">
          <option>Low</option>
          <option selected>Medium</option>
          <option>High</option>
        </select>
      </label>

      <label>Progress: <span id="progress-value">0%</span>
        <input type="range" id="progress" min="0" max="100" value="0">
      </label>

      <div class="form-buttons">
        <button type="submit" id="save-btn">Save Task</button>
        <button type="button" id="clear-btn">Clear</button>
      </div>
    </form>
  </section>

  <!-- Tasks List Panel -->
  <section class="panel list-panel">
    <h2>Tasks</h2>
    <div class="list-controls">
      <input id="search" placeholder="Search by title or tag">
      <select id="sort">
        <option value="due">Sort by due date</option>
        <option value="priority">Sort by priority</option>
        <option value="created">Sort by created</option>
      </select>
    </div>
    <div id="tasks-list" class="tasks-list"></div>
  </section>

  <!-- Daily Timeline Panel -->
  <section class="panel timeline-panel">
    <h2>Daily Schedule</h2>
    <div id="timeline" class="timeline"></div>
  </section>

</main>

<div id="toast" class="toast"></div>
<!-- Inside Add/Edit Task Form -->
<label>Category / Subject
  <input type="text" id="category" placeholder="E.g. Physics, Chemistry">
</label>

<!-- Quote Display -->
<p id="daily-quote" class="quote">“Keep pushing forward!”</p>

<!-- Dark Mode Toggle (Header) -->
<button id="dark-mode-btn" class="btn-small" style="margin-top:10px;">Toggle Dark Mode</button>

<!-- Dashboard Section -->
<section class="panel dashboard-panel">
  <h2>Progress Dashboard</h2>
  <p>Total Tasks: <span id="total-tasks">0</span></p>
  <p>Completed: <span id="completed-tasks">0</span></p>
  <p>Average Progress: <span id="avg-progress">0%</span></p>
</section>

<!-- Filter by Tag / Category -->
<div class="list-controls">
  <input id="search" placeholder="Search by title, tag, or category">
  <select id="sort">
    <option value="due">Sort by due date</option>
    <option value="priority">Sort by priority</option>
    <option value="progress">Sort by progress</option>
  </select>
  <select id="filter-tag">
    <option value="">Filter by tag</option>
  </select>
</div>


<script src="app.js" defer></script>
</body>
</html>
### css code
:root{
  --bg:#f9f9fb;
  --card:#ffffff;
  --accent:#6366f1;
  --accent-dark:#4f46e5;
  --text:#111;
  --muted:#6b7280;
}

*{box-sizing:border-box;margin:0;padding:0;}
body{
  font-family: 'Inter', sans-serif;
  background:var(--bg);
  color:var(--text);
  transition: background 0.3s, color 0.3s;
}

.header{
  text-align:center;
  background:linear-gradient(90deg,var(--accent-dark),#8b5cf6);
  color:#fff;
  padding:20px;
  border-radius:0 0 20px 20px;
}
.header h1{font-size:2rem;}
.header-quote{
  font-style:italic;
  font-size:1rem;
  margin-top:8px;
  opacity:0.9;
}

.main-container{
  display:grid;
  grid-template-columns:1fr 1fr 1fr;
  gap:20px;
  max-width:1200px;
  margin:20px auto;
  padding:0 10px;
}

.panel{
  background:var(--card);
  border-radius:12px;
  padding:20px;
  box-shadow:0 6px 18px rgba(16,24,40,0.06);
  transition: transform 0.2s ease, box-shadow 0.2s ease;
}

.panel:hover{
  transform: translateY(-3px);
  box-shadow:0 12px 24px rgba(16,24,40,0.12);
}

.task-panel form label{
  display:block;
  margin-bottom:12px;
}
.task-panel input[type=text], 
.task-panel input[type=datetime-local],
.task-panel select, 
.task-panel textarea, 
.task-panel input[type=range]{
  width:100%;
  padding:10px;
  border-radius:8px;
  border:1px solid #e6e9f2;
  margin-top:4px;
  transition: border 0.2s ease, box-shadow 0.2s ease;
}

input:focus, textarea:focus, select:focus{
  border-color: var(--accent-dark);
  box-shadow: 0 0 5px rgba(99,102,241,0.3);
  outline: none;
}

.form-buttons{
  display:flex;
  gap:10px;
  margin-top:10px;
}
.form-buttons button{
  flex:1;
  padding:10px;
  border:none;
  border-radius:10px;
  background:var(--accent-dark);
  color:#fff;
  cursor:pointer;
  transition: background 0.2s ease, transform 0.2s ease;
}

.form-buttons button:hover{
  background:#7c3aed;
  transform: scale(1.05);
}

.list-controls{
  display:flex;
  gap:10px;
  margin-bottom:10px;
}
.list-controls input, .list-controls select{
  padding:8px;
  border-radius:8px;
  border:1px solid #e6e9f2;
}

.tasks-list{
  display:flex;
  flex-direction:column;
  gap:12px;
  max-height:70vh;
  overflow:auto;
}

.task-card{
  background:#f5f5ff;
  padding:14px;
  border-radius:12px;
  border-left:4px solid var(--accent-dark);
  display:flex;
  flex-direction:column;
  transition: transform 0.2s ease, box-shadow 0.2s ease;
}

.task-card:hover{
  transform: translateY(-4px);
  box-shadow:0 10px 25px rgba(16,24,40,0.15);
}

.task-title{
  font-weight:600;
  font-size:1rem;
}
.task-meta{
  font-size:0.85rem;
  color:var(--muted);
  margin-top:4px;
}

.task-controls{
  margin-top:8px;
  display:flex;
  gap:8px;
}
.btn-small{
  background:var(--accent);
  color:#fff;
  border:none;
  border-radius:8px;
  padding:6px 10px;
  cursor:pointer;
  font-size:0.85rem;
  transition: background 0.2s ease, transform 0.2s ease;
}
.btn-small:hover{
  background: #4f46e5;
  transform: scale(1.05);
}

.timeline-panel #timeline{
  display:flex;
  flex-direction:column;
  gap:10px;
  max-height:75vh;
  overflow:auto;
}
.timeline-card{
  padding:12px;
  border-radius:12px;
  background:#eef2ff;
  border-left:4px solid var(--accent-dark);
  display:flex;
  justify-content:space-between;
  transition: transform 0.2s ease, box-shadow 0.2s ease, border-left-color 0.2s ease;
}
.timeline-card:hover{
  transform: translateX(4px);
  box-shadow: 0 8px 20px rgba(16,24,40,0.1);
  border-left-color: #8b5cf6;
}

.progress-bar{
  background:#ddd;
  border-radius:6px;
  height:6px;
  margin-top:6px;
  overflow:hidden;
}
.progress-inner{
  height:100%;
  background:linear-gradient(90deg,var(--accent-dark),#8b5cf6);
  width:0;
  transition: width 0.5s ease, background 0.3s ease;
}

.quote{
  font-style:italic;
  color:var(--accent-dark);
  background:#eef2ff;
  padding:8px 12px;
  border-radius:8px;
  margin-bottom:12px;
  text-align:center;
  font-size:0.95rem;
}

.dashboard-panel p{
  font-size:0.95rem;
  margin:6px 0;
}

.toast{
  position:fixed;
  bottom:20px;
  right:20px;
  background:#111;
  color:#fff;
  padding:14px 18px;
  border-radius:8px;
  opacity:0;
  transform:translateY(12px);
  transition:all .25s;
}
.toast.show{
  opacity:1;
  transform:none;
}

body.dark-mode{
  background:#1f2937;
  color:#f3f4f6;
}
body.dark-mode .panel{
  background:#374151;
  color:#f3f4f6;
}
body.dark-mode input, body.dark-mode textarea, body.dark-mode select{
  background:#4b5563; color:#f3f4f6; border:1px solid #6b7280;
}

@media(max-width:1000px){
  .main-container{
    grid-template-columns:1fr;
  }
  .timeline-panel{order:3;}
}
.task-panel {
  background: #fef3c7; /* light yellow */
  border-left: 4px solid #f59e0b; /* amber accent */
}

.list-panel {
  background: #d1fae5; /* light green */
  border-left: 4px solid #10b981; /* green accent */
}

.timeline-panel {
  background: #dbeafe; /* light blue */
  border-left: 4px solid #3b82f6; /* blue accent */
}

.dashboard-panel {
  background: #fce7f3; /* light pink */
  border-left: 4px solid #ec4899; /* pink accent */
}
/* Add to your styles.css */
.task-card.overdue { border-left-color: #ef4444; }    /* red */
.task-card.upcoming-soon { border-left-color: #facc15; } /* yellow */
.task-card.upcoming { border-left-color: #10b981; }   /* green */
:root {
  --bg: #f3f4f6;
  --card-bg: #fff;
  --accent-dark: #7c3aed;
  --accent-light: #8b5cf6;
  --text-color: #111827;
  --overdue-red: #ef4444;
  --upcoming-yellow: #facc15;
  --upcoming-green: #10b981;
  --border-radius: 10px;
  --transition-speed: 0.3s;
}

body {
  background: var(--bg);
  font-family: 'Inter', sans-serif;
  color: var(--text-color);
  margin: 0;
  padding: 0;
}

.task-card {
  background: var(--card-bg);
  border-left: 5px solid var(--accent-dark);
  border-radius: var(--border-radius);
  padding: 15px;
  margin-bottom: 15px;
  box-shadow: 0 3px 6px rgba(0,0,0,0.1);
  transition: transform var(--transition-speed), box-shadow var(--transition-speed);
}

.task-card:hover {
  transform: translateY(-3px);
  box-shadow: 0 8px 20px rgba(0,0,0,0.15);
}

.task-card .task-title {
  font-weight: 600;
  font-size: 1.1rem;
  margin-bottom: 5px;
}

.task-card .task-meta {
  font-size: 0.85rem;
  color: #6b7280;
  margin-bottom: 5px;
}

.progress-bar {
  background: #e5e7eb;
  height: 8px;
  border-radius: 4px;
  overflow: hidden;
  margin: 8px 0;
}

.progress-inner {
  height: 100%;
  border-radius: 4px;
  transition: width var(--transition-speed) ease, background var(--transition-speed);
}

.task-controls button {
  padding: 5px 10px;
  margin-right: 5px;
  border: none;
  border-radius: 5px;
  background: var(--accent-dark);
  color: white;
  cursor: pointer;
  transition: background var(--transition-speed), transform var(--transition-speed);
}

.task-controls button:hover {
  background: var(--accent-light);
  transform: scale(1.05);
}

/* Overdue task border */
.task-card.overdue { border-left-color: var(--overdue-red); }

/* Upcoming tasks border */
.task-card.upcoming-soon { border-left-color: var(--upcoming-yellow); }
.task-card.upcoming { border-left-color: var(--upcoming-green); }

/* Timeline cards */
.timeline-card {
  background: var(--card-bg);
  border-radius: var(--border-radius);
  padding: 10px;
  margin-bottom: 10px;
  box-shadow: 0 2px 4px rgba(0,0,0,0.08);
  transition: transform var(--transition-speed), box-shadow var(--transition-speed);
}

.timeline-card:hover {
  transform: translateY(-2px);
  box-shadow: 0 6px 12px rgba(0,0,0,0.12);
}

/* Toast notifications */
#toast {
  position: fixed;
  bottom: 20px;
  left: 50%;
  transform: translateX(-50%);
  background: var(--accent-dark);
  color: white;
  padding: 12px 20px;
  border-radius: var(--border-radius);
  opacity: 0;
  pointer-events: none;
  transition: opacity 0.3s ease;
}

#toast.show { opacity: 1; pointer-events: auto; }

/* Dark mode */
body.dark-mode {
  background: #111827;
  color: #f9fafb;
}

body.dark-mode .task-card, body.dark-mode .timeline-card {
  background: #1f2937;
  color: #f9fafb;
}

body.dark-mode .task-controls button {
  background: #7c3aed;
}

body.dark-mode .task-controls button:hover {
  background: #8b5cf6;
}
.overdue { border-left-color: red; }
.upcoming-soon { border-left-color: #facc15; } /* yellow */
.upcoming { border-left-color: #10b981; } /* green */

#### java script code
(() => {
  const STORAGE_KEY = 'smartStudyPlanner.tasks';
  let tasks = [];
  let editingId = null;
  const $ = id => document.getElementById(id);

  // ------------------- Storage -------------------
  function saveTasks(){ localStorage.setItem(STORAGE_KEY, JSON.stringify(tasks)); }
  function loadTasks(){ try { const raw = localStorage.getItem(STORAGE_KEY); return raw ? JSON.parse(raw) : []; } catch(e){ return []; } }

  // ------------------- Utilities -------------------
  function fmtDate(iso){ if(!iso) return 'No deadline'; return new Date(iso).toLocaleString(); }
  function showToast(msg,duration=4000){ const t=$('toast'); if(!t) return; t.textContent=msg; t.classList.add('show'); setTimeout(()=>t.classList.remove('show'),duration); }

  // ------------------- Inspirational Quote -------------------
  const quotes = [
    "Don't watch the clock; do what it does. Keep going.",
    "Success is the sum of small efforts repeated day in and day out.",
    "The secret of getting ahead is getting started.",
    "Start where you are. Use what you have. Do what you can."
  ];

  // ------------------- CRUD Tasks -------------------
  function addTask(obj){ obj.id = Date.now(); obj.createdAt = new Date().toISOString(); obj.notified=false; tasks.push(obj); saveTasks(); render(); showToast('Task added'); }
  function updateTask(id, patch){ tasks = tasks.map(t => t.id===id ? {...t,...patch} : t); saveTasks(); render(); showToast('Task updated'); }
  function deleteTask(id){ tasks = tasks.filter(t=>t.id!==id); saveTasks(); render(); }
  function toggleComplete(id){ tasks = tasks.map(t => t.id===id ? {...t,completed:!t.completed} : t); saveTasks(); render(); }

  // ------------------- Dashboard -------------------
  function updateDashboard(){
    const total = tasks.length;
    const completed = tasks.filter(t=>t.completed).length;
    const avg = total ? Math.round(tasks.reduce((acc,t)=>acc+t.progress,0)/total) : 0;
    if($('total-tasks')) $('total-tasks').textContent = total;
    if($('completed-tasks')) $('completed-tasks').textContent = completed;
    if($('avg-progress')) $('avg-progress').textContent = avg+'%';
  }

  // ------------------- Render Tasks List -------------------
  function renderTasksList(){
    const container = $('tasks-list'); if(!container) return;
    container.innerHTML = '';
    const list = tasks.slice();

    if(list.length === 0){ container.innerHTML = '<p style="opacity:.6">No tasks found</p>'; return; }

    list.forEach(task=>{
      const card = document.createElement('div'); card.className='task-card';

      const now = new Date();
      const due = task.dueDate ? new Date(task.dueDate) : null;
      const overdue = due && !task.completed && due < now;
      const upcomingSoon = due && !task.completed && due > now && (due - now <= 12*60*60*1000);

      if(overdue) card.classList.add('overdue');
      else if(upcomingSoon) card.classList.add('upcoming-soon');
      else card.classList.add('upcoming');

      card.innerHTML = `
        <div class="task-title">${task.title} ${task.completed ? '<span style="color:green">(Done)</span>':''}</div>
        <div class="task-meta">${task.description || ''}</div>
        <div class="task-meta">Category: ${task.category || ''} • Tags: ${(task.tags || []).join(', ')} • Due: ${due ? due.toLocaleString() : 'No deadline'}</div>
        <div class="progress-bar"><div class="progress-inner" style="width:${task.progress || 0}%"></div></div>
        <div class="task-controls">
          <button onclick="toggleComplete(${task.id})">${task.completed?'Undo':'Done'}</button>
          <button onclick="startEdit(${task.id})">Edit</button>
          <button onclick="if(confirm('Delete?')) deleteTask(${task.id})">Delete</button>
        </div>
      `;
      container.appendChild(card);
    });

    populateTagFilter();
    updateDashboard();
  }

  // ------------------- Timeline -------------------
  function renderTimeline(){
    const el = $('timeline'); if(!el) return; el.innerHTML='';
    const upcoming = tasks.slice().filter(t=>!t.completed && t.dueDate).sort((a,b)=>new Date(a.dueDate)-new Date(b.dueDate));
    if(upcoming.length===0){ el.innerHTML='<p style="opacity:.6">No upcoming tasks</p>'; return; }
    upcoming.forEach(t=>{
      const daysLeft = Math.ceil((new Date(t.dueDate)-new Date())/(1000*60*60*24));
      const card=document.createElement('div'); card.className='timeline-card';
      card.innerHTML = `<strong>${t.title}</strong> • ${fmtDate(t.dueDate)} <span style="color:${daysLeft<0?'red':'green'}">${daysLeft>=0?daysLeft+' days left':'Overdue '+Math.abs(daysLeft)+' days'}</span>`;
      el.appendChild(card);
    });
  }

  // ------------------- Edit Form -------------------
  function startEdit(id){
    const t = tasks.find(x=>x.id===id); if(!t) return; editingId=id;
    $('task-id').value=t.id;
    $('title').value=t.title;
    $('description').value=t.description||'';
    $('dueDate').value=t.dueDate?t.dueDate.slice(0,16):'';
    $('priority').value=t.priority||'Medium';
    $('category').value=t.category||'';
    $('tags').value=(t.tags||[]).join(',');
    $('progress').value=t.progress||0; $('progress-value').textContent=(t.progress||0)+'%';
    $('save-btn').textContent='Update Task'; window.scrollTo({top:0,behavior:'smooth'});
  }
  function clearForm(){
    editingId=null; $('task-id').value=''; $('title').value=''; $('description').value='';
    $('dueDate').value=''; $('priority').value='Medium'; $('category').value=''; $('tags').value='';
    $('progress').value=0; $('progress-value').textContent='0%'; $('save-btn').textContent='Save Task';
  }

  // ------------------- Tag Filter -------------------
  function populateTagFilter(){
    const filter = $('filter-tag'); if(!filter) return;
    const tags = new Set(); tasks.forEach(t=>t.tags?.forEach(tag=>tags.add(tag)));
    const val = filter.value;
    filter.innerHTML = '<option value="">Filter by tag</option>';
    tags.forEach(tag=>{ const opt = document.createElement('option'); opt.value=tag; opt.textContent=tag; filter.appendChild(opt); });
    filter.value = val;
  }

  // ------------------- Notifications -------------------
  function requestNotificationPermission(){ if('Notification' in window && Notification.permission==='default') Notification.requestPermission(); }
  function checkReminders(){
    const now=Date.now(); let changed=false;
    tasks.forEach(t=>{
      if(!t.dueDate || t.notified || t.completed) return;
      const remindAt = new Date(t.dueDate).getTime() - (t.reminder||30)*60000;
      if(now>=remindAt){ notifyUser(`${t.title} is due!`, t.description||''); t.notified=true; changed=true; }
    });
    if(changed) saveTasks();
  }
  function notifyUser(title, body){ if('Notification' in window && Notification.permission==='granted'){ new Notification(title,{body}); } else{ showToast(title+' — '+body); } }

  // ------------------- Daily Quote -------------------
  function showDailyQuote(){ $('daily-quote') && ($('daily-quote').textContent = quotes[Math.floor(Math.random()*quotes.length)]); }

  // ------------------- Init -------------------
  function init(){
    tasks = loadTasks();

    // ---------- Add 3 demo tasks: 1 overdue, 2 upcoming ----------
    const demoTasks = [
      {
        id: Date.now() + 100,
        title: "Overdue: Physics Quiz",
        description: "Revise chapters 3 and 4 for yesterday's quiz",
        dueDate: new Date(Date.now() - 24*60*60*1000).toISOString(),
        priority: "High",
        category: "Physics",
        tags: ["Quiz"],
        progress: 50,
        completed: false,
        createdAt: new Date().toISOString(),
        notified: false
      },
      {
        id: Date.now() + 101,
        title: "Upcoming: Chemistry Assignment",
        description: "Complete last 5 questions from workbook",
        dueDate: new Date(Date.now() + 6*60*60*1000).toISOString(),
        priority: "Medium",
        category: "Chemistry",
        tags: ["Homework"],
        progress: 10,
        completed: false,
        createdAt: new Date().toISOString(),
        notified: false
      },
      {
        id: Date.now() + 102,
        title: "Upcoming: Math Practice Test",
        description: "Practice previous year questions",
        dueDate: new Date(Date.now() + 24*60*60*1000).toISOString(),
        priority: "High",
        category: "Math",
        tags: ["Test","Practice"],
        progress: 0,
        completed: false,
        createdAt: new Date().toISOString(),
        notified: false
      }
    ];
    tasks = tasks.concat(demoTasks);
    saveTasks();

    renderTasksList();
    renderTimeline();
    showDailyQuote();
    updateDashboard();
    requestNotificationPermission();

    // ---------- Event Listeners ----------
    $('task-form')?.addEventListener('submit', e=>{
      e.preventDefault();
      const obj = {
        title:$('title').value.trim(),
        description:$('description').value.trim(),
        dueDate:$('dueDate').value?new Date($('dueDate').value).toISOString():null,
        priority:$('priority').value,
        category:$('category').value.trim(),
        tags:$('tags').value.split(',').map(s=>s.trim()).filter(Boolean),
        progress:Math.min(100,Math.max(0,Number($('progress').value))),
        completed:false,
        reminder:30
      };
      if(!obj.title){ showToast('Title required'); return; }
      if(editingId){ updateTask(editingId,obj); } else { addTask(obj); }
      clearForm();
    });

    $('clear-btn')?.addEventListener('click', clearForm);
    $('progress')?.addEventListener('input', ()=> $('progress-value').textContent = $('progress').value+'%');
    $('search')?.addEventListener('input', renderTasksList);
    $('sort')?.addEventListener('change', renderTasksList);
    $('filter-tag')?.addEventListener('change', renderTasksList);
    $('dark-mode-btn')?.addEventListener('click', ()=>document.body.classList.toggle('dark-mode'));
    $('export-btn')?.addEventListener('click', exportTasks);
    $('import-btn')?.addEventListener('click', ()=> $('import-file').click());
    $('import-file')?.addEventListener('change', e=>{ if(e.target.files.length) importTasks(e.target.files[0]); });

    setInterval(checkReminders,60000);
  }

  function render(){ renderTasksList(); renderTimeline(); updateDashboard(); }

  window.addEventListener('DOMContentLoaded',init);
  window.toggleComplete = toggleComplete;
  window.startEdit = startEdit;
  window.deleteTask = deleteTask;

})();
