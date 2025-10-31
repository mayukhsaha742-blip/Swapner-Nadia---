# Swapner Nadia - স্বপ্নের নদীয়া
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Swapner Nadia NGO Portal</title>
  <style>
    body {
      font-family: 'Segoe UI', sans-serif;
      background: linear-gradient(135deg, #dbeafe, #fce7f3);
      margin: 0;
      padding: 0;
      color: #333;
    }
    header {
      background: #6d28d9;
      color: white;
      text-align: center;
      padding: 20px;
      font-size: 24px;
    }
    section {
      background: white;
      border-radius: 16px;
      padding: 20px;
      margin: 20px auto;
      max-width: 700px;
      box-shadow: 0 4px 10px rgba(0,0,0,0.1);
    }
    h2 { color: #4c1d95; }
    input, button {
      width: 100%;
      padding: 10px;
      margin: 5px 0 15px;
      border-radius: 8px;
      border: 1px solid #ccc;
      font-size: 16px;
    }
    button {
      background: #6d28d9;
      color: white;
      border: none;
      cursor: pointer;
      transition: background 0.3s;
    }
    button:hover { background: #4c1d95; }
    ul { list-style: none; padding: 0; }
    li {
      background: #ede9fe;
      margin: 5px 0;
      padding: 10px;
      border-radius: 10px;
      display: flex;
      justify-content: space-between;
      align-items: center;
    }
    li span { flex-grow: 1; }
    .actions button {
      background: none;
      border: none;
      cursor: pointer;
      font-size: 16px;
      margin-left: 10px;
    }
    .actions button:hover { color: #6d28d9; }
  </style>
</head>
<body>
  <header>🌿 Swapner Nadia NGO Portal 🌿</header>

  <!-- Upcoming Programmes Section (now first) -->
  <section>
    <h2>📅 Upcoming Programmes</h2>
    <ul>
      <li>Free Eye Checkup Camp — 15 Nov 2025</li>
      <li>Blood Donation Drive — 2 Dec 2025</li>
      <li>Tree Plantation — 20 Dec 2025</li>
    </ul>
  </section>

  <!-- Member Section (second) -->
  <section>
    <h2>🤝 Join as a Member</h2>
    <input type="text" id="memName" placeholder="Full Name" />
    <input type="email" id="memEmail" placeholder="Email" />
    <input type="text" id="memPhone" placeholder="Phone" />
    <button id="memBtn">Register Member</button>

    <h3>👥 Registered Members:</h3>
    <ul id="memberList"></ul>
  </section>

  <script>
    document.addEventListener('DOMContentLoaded', function() {
      // Load stored members
      let members = JSON.parse(localStorage.getItem('members')) || [];
      const memBtn = document.getElementById('memBtn');

      function showMembers() {
        const list = document.getElementById('memberList');
        list.innerHTML = '';
        if (members.length === 0) list.innerHTML = '<li><em>No members yet</em></li>';
        members.forEach((m, i) => {
          const li = document.createElement('li');
          li.innerHTML = `
            <span>${m.name} — ${m.email} — ${m.phone}</span>
            <div class="actions">
              <button onclick="editMember(${i})">✏️</button>
              <button onclick="deleteMember(${i})">🗑️</button>
            </div>`;
          list.appendChild(li);
        });
        localStorage.setItem('members', JSON.stringify(members));
      }

      function addMember() {
        const name = document.getElementById('memName').value.trim();
        const email = document.getElementById('memEmail').value.trim();
        const phone = document.getElementById('memPhone').value.trim();
        if (!name || !email || !phone) return alert('Please fill all member details.');
        members.push({ name, email, phone });
        document.getElementById('memName').value = '';
        document.getElementById('memEmail').value = '';
        document.getElementById('memPhone').value = '';
        showMembers();
      }

      window.editMember = function(i) {
        const newName = prompt('Edit name:', members[i].name);
        const newEmail = prompt('Edit email:', members[i].email);
        const newPhone = prompt('Edit phone:', members[i].phone);
        if (newName && newEmail && newPhone) {
          members[i] = { name: newName, email: newEmail, phone: newPhone };
          showMembers();
        }
      }

      window.deleteMember = function(i) {
        if (confirm('Remove this member?')) {
          members.splice(i, 1);
          showMembers();
        }
      }

      memBtn.addEventListener('click', addMember);

      // Initial render
      showMembers();
    });
  </script>
</body>
</html>
