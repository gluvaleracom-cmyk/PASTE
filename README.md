[1paste.html](https://github.com/user-attachments/files/23828141/1paste.html)
<!DOCTYPE html>
<html lang="ru">
<head>
  <meta charset="UTF-8" />
  <title>Панель текстовых заготовок</title>
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <style>
    :root {
      --bg-gradient: linear-gradient(135deg, #b388ff, #7f7bff, #ff8ad4);
      --glass-bg: rgba(255, 255, 255, 0.16);
      --glass-bg-strong: rgba(255, 255, 255, 0.24);
      --border-glass: rgba(255, 255, 255, 0.35);
      --text-main: #fdfdff;
      --text-muted: #d3d3ff;
      --accent: #ff7ac4;
      --accent-soft: rgba(255, 122, 196, 0.3);
      --danger: #ff5c7a;
      --shadow-soft: 0 18px 40px rgba(15, 10, 50, 0.35);
      --radius-xl: 18px;
      --radius-2xl: 26px;
    }

    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
    }

    body {
      font-family: system-ui, -apple-system, BlinkMacSystemFont, "Inter", sans-serif;
      background: var(--bg-gradient);
      min-height: 100vh;
      color: var(--text-main);
      display: flex;
      align-items: stretch;
      justify-content: center;
    }

    #app {
      width: 100%;
      min-height: 100vh;
      display: flex;
      align-items: stretch;
      justify-content: center;
    }

    .layout {
      display: grid;
      grid-template-columns: 280px minmax(0, 1fr);
      gap: 20px;
      width: 100%;
      max-width: 1280px;
      padding: 20px;
    }

    @media (max-width: 900px) {
      .layout {
        grid-template-columns: 1fr;
      }
    }

    /* SIDEBAR */

    .sidebar {
      backdrop-filter: blur(24px);
      background: radial-gradient(circle at top left, rgba(255,255,255,0.24), rgba(101, 86, 255, 0.06));
      border-radius: var(--radius-2xl);
      border: 1px solid var(--border-glass);
      box-shadow: var(--shadow-soft);
      padding: 18px 16px;
      display: flex;
      flex-direction: column;
      gap: 14px;
      overflow: hidden;
    }

    .sidebar-header {
      display: flex;
      flex-direction: column;
      gap: 12px;
    }

    .sidebar-title {
      font-size: 18px;
      font-weight: 600;
      letter-spacing: 0.04em;
      text-transform: uppercase;
      color: #ffffff;
    }

    .search-box {
      background: rgba(15, 10, 40, 0.35);
      border-radius: 999px;
      border: 1px solid rgba(255, 255, 255, 0.2);
      padding: 8px 14px;
      display: flex;
      align-items: center;
      gap: 8px;
    }

    .search-box input {
      background: transparent;
      border: none;
      color: var(--text-main);
      outline: none;
      width: 100%;
      font-size: 13px;
    }

    .search-box input::placeholder {
      color: rgba(230, 230, 255, 0.7);
    }

    .search-icon {
      font-size: 15px;
      opacity: 0.9;
    }

    .sidebar-scroll {
      margin-top: 6px;
      overflow-y: auto;
      padding-right: 4px;
      scrollbar-width: thin;
      scrollbar-color: rgba(255,255,255,0.4) transparent;
    }

    .sidebar-scroll::-webkit-scrollbar {
      width: 4px;
    }

    .sidebar-scroll::-webkit-scrollbar-track {
      background: transparent;
    }

    .sidebar-scroll::-webkit-scrollbar-thumb {
      background: rgba(255,255,255,0.5);
      border-radius: 999px;
    }

    .category {
      margin-bottom: 8px;
    }

    .category-header {
      display: flex;
      align-items: center;
      gap: 6px;
      cursor: pointer;
      padding: 6px 8px;
      border-radius: 999px;
      transition: background 0.18s ease, transform 0.1s ease;
    }

    .category-header:hover {
      background: rgba(255,255,255,0.12);
      transform: translateY(-1px);
    }

    .category-toggle {
      font-size: 10px;
      opacity: 0.9;
      width: 16px;
      text-align: center;
    }

    .category-icon {
      width: 18px;
      height: 18px;
      border-radius: 6px;
      background: rgba(255,255,255,0.2);
      display: flex;
      align-items: center;
      justify-content: center;
      font-size: 11px;
    }

    .category-name {
      font-size: 13px;
      font-weight: 500;
      flex: 1;
      text-transform: uppercase;
      letter-spacing: 0.06em;
    }

    .category-actions {
      display: flex;
      gap: 4px;
      opacity: 0.9;
    }

    .icon-btn {
      background: rgba(15, 10, 40, 0.35);
      border-radius: 999px;
      padding: 3px 7px;
      border: 1px solid rgba(255,255,255,0.3);
      font-size: 11px;
      cursor: pointer;
      display: inline-flex;
      align-items: center;
      justify-content: center;
      transition: background 0.18s ease, transform 0.1s ease, box-shadow 0.1s ease;
      color: var(--text-main);
    }

    .icon-btn:hover {
      background: rgba(255,255,255,0.2);
      transform: translateY(-1px);
      box-shadow: 0 5px 15px rgba(15, 10, 50, 0.35);
    }

    .subcategory-list {
      margin-left: 26px;
      margin-top: 6px;
      padding-left: 8px;
      border-left: 1px solid rgba(255,255,255,0.2);
      display: none;
    }

    .category.expanded .subcategory-list {
      display: block;
    }

    .subcategory-item {
      display: flex;
      align-items: center;
      gap: 6px;
      padding: 5px 8px;
      margin-bottom: 4px;
      border-radius: 999px;
      background: transparent;
      cursor: pointer;
      transition: background 0.17s ease, transform 0.1s ease, box-shadow 0.1s ease;
      font-size: 13px;
    }

    .subcategory-label {
      flex: 1;
    }

    .subcategory-item:hover {
      background: rgba(255,255,255,0.14);
      transform: translateY(-1px);
      box-shadow: 0 10px 18px rgba(15, 10, 50, 0.3);
    }

    .subcategory-item.active {
      background: linear-gradient(135deg, #ff9ad8, #ff7ac4);
      color: #1d1035;
      box-shadow: 0 12px 26px rgba(255, 122, 196, 0.65);
    }

    .subcategory-item.active .icon-btn {
      border-color: rgba(0,0,0,0.3);
      background: rgba(255,255,255,0.6);
      color: #1d1035;
    }

    .subcategory-bullet {
      width: 3px;
      height: 20px;
      border-radius: 999px;
      background: linear-gradient(to bottom, #ffb5e6, rgba(255,255,255,0));
      margin-right: 2px;
    }

    .subcategory-actions {
      display: flex;
      gap: 4px;
    }

    .add-subcategory-row {
      display: flex;
      align-items: center;
      gap: 8px;
      margin-top: 4px;
      padding-left: 5px;
      font-size: 11px;
      color: var(--text-muted);
    }

    .add-subcategory-row button {
      font-size: 12px;
      padding: 2px 8px;
    }

    /* MAIN */

    .main {
      display: flex;
      flex-direction: column;
      gap: 14px;
      position: relative;
    }

    .template-card {
      flex: 1;
      min-height: 0;
      backdrop-filter: blur(26px);
      background: radial-gradient(circle at top left, rgba(255,255,255,0.25), rgba(15,10,60,0.65));
      border-radius: 34px;
      border: 1px solid rgba(255,255,255,0.5);
      box-shadow: 0 24px 60px rgba(10, 5, 40, 0.75);
      padding: 22px 22px 18px;
      display: flex;
      flex-direction: column;
      gap: 14px;
      position: relative;
      overflow: hidden;
    }

    .template-card::before {
      content: "";
      position: absolute;
      inset: 0;
      pointer-events: none;
      background: radial-gradient(circle at top right, rgba(255,255,255,0.26), transparent 55%);
      opacity: 0.9;
      mix-blend-mode: screen;
    }

    .template-header {
      position: relative;
      z-index: 1;
      display: flex;
      justify-content: space-between;
      align-items: center;
      gap: 10px;
    }

    .template-title {
      font-size: 22px;
      font-weight: 600;
      letter-spacing: 0.06em;
      text-transform: uppercase;
    }

    .template-path {
      font-size: 12px;
      color: var(--text-muted);
    }

    .user-chip {
      font-size: 12px;
      padding: 6px 10px;
      border-radius: 999px;
      background: rgba(15,10,40,0.6);
      border: 1px solid rgba(255,255,255,0.35);
      display: inline-flex;
      align-items: center;
      gap: 6px;
    }

    .user-dot {
      width: 7px;
      height: 7px;
      border-radius: 999px;
      background: #5bffb1;
      box-shadow: 0 0 8px rgba(91,255,177,0.9);
    }

    .template-body {
      position: relative;
      z-index: 1;
      flex: 1;
      min-height: 0;
      display: flex;
      flex-direction: column;
      gap: 10px;
    }

    .template-textarea {
      flex: 1;
      width: 100%;
      resize: none;
      border-radius: 22px;
      border: 1px solid rgba(255,255,255,0.6);
      background: rgba(6, 2, 34, 0.6);
      padding: 14px 16px;
      color: var(--text-main);
      font-size: 14px;
      line-height: 1.5;
      outline: none;
      box-shadow: inset 0 0 0 1px rgba(255,255,255,0.06);
      scrollbar-width: thin;
      scrollbar-color: rgba(255,255,255,0.7) transparent;
      white-space: pre-wrap;
    }

    .template-textarea:disabled {
      opacity: 0.65;
    }

    .template-textarea::-webkit-scrollbar {
      width: 5px;
    }

    .template-textarea::-webkit-scrollbar-thumb {
      background: rgba(255, 255, 255, 0.7);
      border-radius: 999px;
    }

    .template-hint {
      font-size: 12px;
      color: var(--text-muted);
      display: flex;
      justify-content: space-between;
      gap: 10px;
      flex-wrap: wrap;
    }

    .template-actions {
      display: flex;
      justify-content: flex-end;
      gap: 10px;
      margin-top: 2px;
    }

    .btn {
      border-radius: 999px;
      border: 1px solid rgba(255,255,255,0.6);
      padding: 7px 16px;
      font-size: 13px;
      cursor: pointer;
      background: rgba(15,10,40,0.7);
      color: var(--text-main);
      display: inline-flex;
      align-items: center;
      gap: 6px;
      transition: background 0.18s ease, transform 0.1s ease, box-shadow 0.1s ease;
    }

    .btn-primary {
      background: linear-gradient(135deg, #ffb6ec, #ff7ac4);
      color: #27113b;
      border-color: transparent;
      box-shadow: 0 14px 28px rgba(255, 122, 196, 0.7);
    }

    .btn-primary:hover {
      transform: translateY(-2px);
      box-shadow: 0 18px 40px rgba(255, 122, 196, 0.9);
    }

    .btn-outline {
      background: rgba(15,10,50,0.6);
    }

    .btn-outline:hover {
      background: rgba(255,255,255,0.14);
      transform: translateY(-1px);
      box-shadow: 0 12px 22px rgba(10, 5, 40, 0.7);
    }

    .bottom-bar {
      position: relative;
      backdrop-filter: blur(20px);
      background: rgba(19, 9, 60, 0.75);
      border-radius: var(--radius-xl);
      border: 1px solid rgba(255,255,255,0.4);
      box-shadow: 0 16px 38px rgba(10,5,40,0.8);
      padding: 10px 12px;
      display: flex;
      justify-content: flex-end;
      align-items: center;
      gap: 10px;
      font-size: 12px;
      color: var(--text-muted);
    }

    /* AUTH SCREEN */

    .auth-screen {
      position: fixed;
      inset: 0;
      background: radial-gradient(circle at top left, rgba(255,255,255,0.06), rgba(0,0,0,0.65));
      backdrop-filter: blur(26px);
      display: flex;
      align-items: center;
      justify-content: center;
      z-index: 50;
    }

    .auth-card {
      width: 100%;
      max-width: 420px;
      background: rgba(18, 8, 60, 0.9);
      border-radius: 28px;
      padding: 22px 22px 18px;
      border: 1px solid rgba(255,255,255,0.5);
      box-shadow: 0 24px 60px rgba(6, 3, 30, 0.9);
      position: relative;
      overflow: hidden;
      color: var(--text-main);
    }

    .auth-card::before {
      content: "";
      position: absolute;
      inset: -30%;
      background: radial-gradient(circle at top right, rgba(255,255,255,0.25), transparent 55%);
      opacity: 0.9;
      mix-blend-mode: screen;
      pointer-events: none;
    }

    .auth-inner {
      position: relative;
      z-index: 1;
    }

    .auth-title {
      font-size: 20px;
      font-weight: 600;
      letter-spacing: 0.08em;
      text-transform: uppercase;
      margin-bottom: 4px;
    }

    .auth-subtitle {
      font-size: 12px;
      color: var(--text-muted);
      margin-bottom: 16px;
    }

    .auth-form-group {
      margin-bottom: 12px;
      display: flex;
      flex-direction: column;
      gap: 6px;
      font-size: 13px;
    }

    .auth-label {
      color: var(--text-muted);
    }

    .auth-input {
      padding: 8px 11px;
      border-radius: 13px;
      border: 1px solid rgba(255,255,255,0.65);
      background: rgba(10, 5, 40, 0.7);
      outline: none;
      color: var(--text-main);
      font-size: 13px;
    }

    .auth-input::placeholder {
      color: rgba(226,226,255,0.7);
    }

    .auth-actions {
      margin-top: 10px;
      display: flex;
      flex-direction: column;
      gap: 8px;
    }

    .auth-row {
      display: flex;
      justify-content: space-between;
      gap: 10px;
      flex-wrap: wrap;
      align-items: center;
      font-size: 12px;
    }

    .auth-link {
      border: none;
      background: none;
      color: var(--accent);
      cursor: pointer;
      padding: 0;
      text-decoration: underline;
      font-size: 12px;
    }

    .auth-link:hover {
      opacity: 0.85;
    }

    .badge-pill {
      padding: 4px 9px;
      border-radius: 999px;
      background: rgba(10,5,40,0.7);
      border: 1px solid rgba(255,255,255,0.55);
      font-size: 11px;
      color: var(--text-muted);
    }

    .hidden {
      display: none !important;
    }

    /* MODAL */

    .modal-backdrop {
      position: fixed;
      inset: 0;
      background: rgba(0,0,0,0.6);
      backdrop-filter: blur(18px);
      display: flex;
      align-items: center;
      justify-content: center;
      z-index: 60;
    }

    .modal {
      width: 100%;
      max-width: 480px;
      background: rgba(18, 8, 60, 0.95);
      border-radius: 26px;
      padding: 18px 18px 14px;
      border: 1px solid rgba(255,255,255,0.6);
      box-shadow: 0 24px 60px rgba(6, 3, 30, 0.9);
      color: var(--text-main);
      position: relative;
    }

    .modal-title {
      font-size: 16px;
      font-weight: 600;
      margin-bottom: 4px;
    }

    .modal-subtitle {
      font-size: 12px;
      color: var(--text-muted);
      margin-bottom: 12px;
    }

    .modal-close {
      position: absolute;
      top: 10px;
      right: 12px;
      border-radius: 999px;
      width: 26px;
      height: 26px;
      border: 1px solid rgba(255,255,255,0.7);
      background: rgba(15,10,40,0.7);
      display: flex;
      align-items: center;
      justify-content: center;
      cursor: pointer;
      font-size: 14px;
      transition: background 0.18s ease, transform 0.1s ease;
    }

    .modal-close:hover {
      background: rgba(255,255,255,0.2);
      transform: translateY(-1px);
    }

    .user-list {
      margin-top: 8px;
      border-radius: 16px;
      background: rgba(10, 5, 40, 0.7);
      border: 1px solid rgba(255,255,255,0.35);
      padding: 8px 10px;
      max-height: 180px;
      overflow-y: auto;
      font-size: 12px;
    }

    .user-row {
      display: flex;
      justify-content: space-between;
      align-items: center;
      gap: 8px;
      padding: 4px 0;
      border-bottom: 1px solid rgba(255,255,255,0.08);
    }

    .user-row:last-child {
      border-bottom: none;
    }

    .user-row-name {
      display: flex;
      flex-direction: column;
      gap: 1px;
    }

    .user-role {
      font-size: 11px;
      color: var(--text-muted);
    }

    .user-remove {
      border-radius: 999px;
      border: 1px solid rgba(255,255,255,0.6);
      background: rgba(130, 20, 50, 0.9);
      color: #fff;
      font-size: 11px;
      padding: 3px 8px;
      cursor: pointer;
      transition: background 0.18s ease, transform 0.1s ease;
    }

    .user-remove:hover {
      background: var(--danger);
      transform: translateY(-1px);
    }

    .pill-label {
      font-size: 11px;
      padding: 2px 8px;
      border-radius: 999px;
      background: rgba(255,255,255,0.18);
      color: #160a33;
    }

  </style>
</head>
<body>
<div id="app">

  <!-- AUTH SCREEN -->
  <div id="authScreen" class="auth-screen">
    <div class="auth-card">
      <div class="auth-inner">
        <div class="auth-title">Панель заготовок</div>
        <div class="auth-subtitle">
          Доступ только для пользователей, созданных через администратора.
        </div>

        <form id="loginForm">
          <div class="auth-form-group">
            <label class="auth-label" for="loginUsername">Логин</label>
            <input id="loginUsername" class="auth-input" type="text" autocomplete="username" required placeholder="например, operator01" />
          </div>
          <div class="auth-form-group">
            <label class="auth-label" for="loginPassword">Пароль</label>
            <input id="loginPassword" class="auth-input" type="password" autocomplete="current-password" required placeholder="Введите пароль" />
          </div>
          <div class="auth-actions">
            <button type="submit" class="btn btn-primary" style="width:100%; justify-content:center;">
              Войти в панель
            </button>
            <div class="auth-row">
              <span class="badge-pill">Создание учёток — через администратора</span>
              <button type="button" id="openAdminPanelBtn" class="auth-link">
                Открыть панель администратора
              </button>
            </div>
          </div>
        </form>
      </div>
    </div>
  </div>

  <!-- ADMIN MODAL -->
  <div id="adminModalBackdrop" class="modal-backdrop hidden">
    <div class="modal">
      <button class="modal-close" id="closeAdminModalBtn">✕</button>
      <div id="adminStepPassword">
        <div class="modal-title">Админ-панель</div>
        <div class="modal-subtitle">
          Введите админ-пароль, чтобы управлять пользователями панели.
        </div>
        <form id="adminPasswordForm">
          <div class="auth-form-group">
            <label class="auth-label" for="adminPasswordInput">Админ-пароль</label>
            <input id="adminPasswordInput" class="auth-input" type="password" autocomplete="off" required />
          </div>
          <div class="auth-actions">
            <button type="submit" class="btn btn-primary">Продолжить</button>
          </div>
        </form>
      </div>

      <div id="adminStepManage" class="hidden">
        <div class="modal-title">Управление пользователями</div>
        <div class="modal-subtitle">
          Создавайте логины и пароли, которые будут использоваться для входа на сайт.
        </div>
        <form id="createUserForm">
          <div class="auth-form-group">
            <label class="auth-label" for="newUsername">
              Новый логин <span class="pill-label">оператор</span>
            </label>
            <input id="newUsername" class="auth-input" type="text" autocomplete="off" required placeholder="например, operator01" />
          </div>
          <div class="auth-form-group">
            <label class="auth-label" for="newPassword">Пароль</label>
            <input id="newPassword" class="auth-input" type="password" autocomplete="off" required placeholder="Придумайте пароль" />
          </div>
          <div class="auth-actions">
            <button type="submit" class="btn btn-primary">Создать пользователя</button>
          </div>
        </form>

        <div class="user-list" id="userList"></div>
      </div>
    </div>
  </div>

  <!-- MAIN LAYOUT -->
  <div class="layout">
    <!-- SIDEBAR -->
    <aside class="sidebar">
      <div class="sidebar-header">
        <div class="sidebar-title">Разделы</div>
        <div class="search-box">
          <span class="search-icon">🔎</span>
          <input id="searchInput" type="text" placeholder="Поиск по подпапкам..." />
        </div>
      </div>
      <div id="sidebarContainer" class="sidebar-scroll">
        <!-- Категории и подпапки будут отрисованы JS -->
      </div>
    </aside>

    <!-- MAIN -->
    <main class="main">
      <section class="template-card">
        <div class="template-header">
          <div>
            <div class="template-title" id="templateTitle">Выберите заготовку</div>
            <div class="template-path" id="templatePath">Раздел / подпапка</div>
          </div>
          <div class="user-chip">
            <span class="user-dot"></span>
            <span id="currentUserLabel">Не авторизовано</span>
          </div>
        </div>

        <div class="template-body">
          <textarea id="templateText"
                    class="template-textarea"
                    placeholder="Выберите подпапку слева или создайте новую, чтобы редактировать текст заготовки."
                    disabled></textarea>
          <div class="template-hint">
            <span id="currentTemplateHint">Нет выбранной заготовки</span>
            <span>Изменения сохраняются в браузере (localStorage).</span>
          </div>
          <div class="template-actions">
            <button id="saveTemplateBtn" class="btn btn-primary" disabled>Сохранить изменения</button>
          </div>
        </div>
      </section>

      <footer class="bottom-bar">
        <span>Если что-то пошло не так — обновите панель.</span>
        <button id="refreshBtn" class="btn btn-outline">Обновить</button>
      </footer>
    </main>
  </div>
</div>

<script>
  // ====== DATA & CONSTANTS ======
  const ADMIN_PASSWORD = "qwerty1234";

  const CATEGORY_ORDER = [
    "РАССЫЛКИ",
    "ВЧ",
    "КАСТОМ",
    "ПЛАТКИ",
    "ОФФЕРЫ",
    "СЕКСИНГ",
    "РАБЫ",
    "ПРОБЛЕМЫ",
    "ФАКЛИСТ",
    "БАНДЛЫ",
    "ВОПРОСЫ",
    "ДИКРЕЙТ"
  ];

  const TEMPLATE_STORAGE_KEY = "templateData_v3";
  const USERS_STORAGE_KEY = "panelUsers_v1";

  let templateData = {};
  let currentUser = null;
  let currentCategory = null;
  let currentSubcategory = null;

  // ====== LOCAL STORAGE HELPERS ======
  function loadUsers() {
    let users = localStorage.getItem(USERS_STORAGE_KEY);
    if (!users) {
      // создаём дефолтного админа, если совсем пусто
      const defaultUsers = [
        { username: "admin", password: ADMIN_PASSWORD, role: "admin" }
      ];
      localStorage.setItem(USERS_STORAGE_KEY, JSON.stringify(defaultUsers));
      return defaultUsers;
    }
    try {
      return JSON.parse(users) || [];
    } catch (e) {
      return [];
    }
  }

  function saveUsers(users) {
    localStorage.setItem(USERS_STORAGE_KEY, JSON.stringify(users));
  }

  function loadTemplateData() {
    let dataStr = localStorage.getItem(TEMPLATE_STORAGE_KEY);
    if (!dataStr) {
      const initial = {};
      CATEGORY_ORDER.forEach(cat => {
        initial[cat] = {
          "Пример 1": `Это пример заготовки в разделе «${cat}».\n\nВы можете отредактировать текст, а также создавать свои подпапки и заготовки.`
        };
      });
      templateData = initial;
      saveTemplateData();
      return;
    }
    try {
      templateData = JSON.parse(dataStr) || {};
    } catch (e) {
      templateData = {};
    }

    // гарантия, что все разделы существуют
    CATEGORY_ORDER.forEach(cat => {
      if (!templateData[cat]) {
        templateData[cat] = {};
      }
    });
  }

  function saveTemplateData() {
    localStorage.setItem(TEMPLATE_STORAGE_KEY, JSON.stringify(templateData));
  }

  // ====== AUTH & ADMIN ======

  const authScreen = document.getElementById("authScreen");
  const loginForm = document.getElementById("loginForm");
  const loginUsername = document.getElementById("loginUsername");
  const loginPassword = document.getElementById("loginPassword");
  const currentUserLabel = document.getElementById("currentUserLabel");

  loginForm.addEventListener("submit", (e) => {
    e.preventDefault();
    const username = loginUsername.value.trim();
    const password = loginPassword.value;

    const users = loadUsers();
    const found = users.find(
      u => u.username === username && u.password === password
    );

    if (!found) {
      alert("Неверный логин или пароль.");
      return;
    }

    currentUser = found;
    currentUserLabel.textContent = `Войти как ${found.username}`;
    authScreen.classList.add("hidden");
  });

  // ADMIN MODAL

  const adminModalBackdrop = document.getElementById("adminModalBackdrop");
  const openAdminPanelBtn = document.getElementById("openAdminPanelBtn");
  const closeAdminModalBtn = document.getElementById("closeAdminModalBtn");
  const adminStepPassword = document.getElementById("adminStepPassword");
  const adminStepManage = document.getElementById("adminStepManage");
  const adminPasswordForm = document.getElementById("adminPasswordForm");
  const adminPasswordInput = document.getElementById("adminPasswordInput");
  const createUserForm = document.getElementById("createUserForm");
  const userList = document.getElementById("userList");

  openAdminPanelBtn.addEventListener("click", () => {
    adminModalBackdrop.classList.remove("hidden");
    adminStepPassword.classList.remove("hidden");
    adminStepManage.classList.add("hidden");
    adminPasswordInput.value = "";
    adminPasswordInput.focus();
  });

  closeAdminModalBtn.addEventListener("click", () => {
    adminModalBackdrop.classList.add("hidden");
  });

  adminModalBackdrop.addEventListener("click", (e) => {
    if (e.target === adminModalBackdrop) {
      adminModalBackdrop.classList.add("hidden");
    }
  });

  adminPasswordForm.addEventListener("submit", (e) => {
    e.preventDefault();
    const pwd = adminPasswordInput.value;
    if (pwd !== ADMIN_PASSWORD) {
      alert("Неверный админ-пароль.");
      return;
    }
    adminStepPassword.classList.add("hidden");
    adminStepManage.classList.remove("hidden");
    renderUserList();
  });

  function renderUserList() {
    const users = loadUsers();
    userList.innerHTML = "";
    if (!users.length) {
      userList.textContent = "Пользователи ещё не созданы.";
      return;
    }
    users.forEach((user, index) => {
      const row = document.createElement("div");
      row.className = "user-row";

      const info = document.createElement("div");
      info.className = "user-row-name";

      const nameLine = document.createElement("div");
      nameLine.textContent = user.username;

      const roleLine = document.createElement("div");
      roleLine.className = "user-role";
      roleLine.textContent = user.role === "admin" ? "Администратор" : "Оператор";

      info.appendChild(nameLine);
      info.appendChild(roleLine);

      row.appendChild(info);

      if (user.role !== "admin") {
        const removeBtn = document.createElement("button");
        removeBtn.className = "user-remove";
        removeBtn.textContent = "Удалить";
        removeBtn.addEventListener("click", () => {
          const usersArr = loadUsers();
          usersArr.splice(index, 1);
          saveUsers(usersArr);
          renderUserList();
        });
        row.appendChild(removeBtn);
      } else {
        const adminTag = document.createElement("div");
        adminTag.className = "pill-label";
        adminTag.textContent = "Админ";
        row.appendChild(adminTag);
      }

      userList.appendChild(row);
    });
  }

  createUserForm.addEventListener("submit", (e) => {
    e.preventDefault();
    const username = document.getElementById("newUsername").value.trim();
    const password = document.getElementById("newPassword").value;

    if (!username || !password) {
      alert("Введите логин и пароль.");
      return;
    }

    const users = loadUsers();
    if (users.find(u => u.username === username)) {
      alert("Пользователь с таким логином уже существует.");
      return;
    }

    users.push({ username, password, role: "user" });
    saveUsers(users);
    document.getElementById("newUsername").value = "";
    document.getElementById("newPassword").value = "";
    renderUserList();
    alert("Пользователь создан. Передайте логин и пароль оператору.");
  });

  // ====== SIDEBAR & TEMPLATES ======

  const sidebarContainer = document.getElementById("sidebarContainer");
  const searchInput = document.getElementById("searchInput");
  const templateTitle = document.getElementById("templateTitle");
  const templatePath = document.getElementById("templatePath");
  const templateText = document.getElementById("templateText");
  const currentTemplateHint = document.getElementById("currentTemplateHint");
  const saveTemplateBtn = document.getElementById("saveTemplateBtn");
  const refreshBtn = document.getElementById("refreshBtn");

  refreshBtn.addEventListener("click", () => {
    location.reload();
  });

  function renderSidebar(filter = "") {
    sidebarContainer.innerHTML = "";
    const filterLower = filter.trim().toLowerCase();

    CATEGORY_ORDER.forEach(catName => {
      const catSub = templateData[catName] || {};

      const categoryEl = document.createElement("div");
      categoryEl.className = "category";
      categoryEl.dataset.category = catName;

      const header = document.createElement("div");
      header.className = "category-header";

      const toggle = document.createElement("div");
      toggle.className = "category-toggle";
      toggle.textContent = "▸";

      const icon = document.createElement("div");
      icon.className = "category-icon";
      icon.textContent = "📁";

      const nameSpan = document.createElement("div");
      nameSpan.className = "category-name";
      nameSpan.textContent = catName;

      const actions = document.createElement("div");
      actions.className = "category-actions";

      const addBtn = document.createElement("button");
      addBtn.className = "icon-btn";
      addBtn.title = "Добавить подпапку";
      addBtn.textContent = "+";
      addBtn.addEventListener("click", (e) => {
        e.stopPropagation();
        addSubcategory(catName);
      });

      actions.appendChild(addBtn);

      header.appendChild(toggle);
      header.appendChild(icon);
      header.appendChild(nameSpan);
      header.appendChild(actions);

      header.addEventListener("click", () => {
        const expanded = categoryEl.classList.toggle("expanded");
        toggle.textContent = expanded ? "▾" : "▸";
      });

      const subList = document.createElement("div");
      subList.className = "subcategory-list";

      const subNames = Object.keys(catSub);
      subNames.forEach(subName => {
        const passesFilter =
          !filterLower ||
          subName.toLowerCase().includes(filterLower) ||
          catName.toLowerCase().includes(filterLower);

        if (!passesFilter) return;

        const item = document.createElement("div");
        item.className = "subcategory-item";
        item.dataset.category = catName;
        item.dataset.subcategory = subName;

        if (currentCategory === catName && currentSubcategory === subName) {
          item.classList.add("active");
        }

        const bullet = document.createElement("div");
        bullet.className = "subcategory-bullet";

        const label = document.createElement("div");
        label.className = "subcategory-label";
        label.textContent = subName;

        const actions = document.createElement("div");
        actions.className = "subcategory-actions";

        const editBtn = document.createElement("button");
        editBtn.className = "icon-btn";
        editBtn.title = "Переименовать подпапку";
        editBtn.textContent = "✎";
        editBtn.addEventListener("click", (e) => {
          e.stopPropagation();
          renameSubcategory(catName, subName);
        });

        const deleteBtn = document.createElement("button");
        deleteBtn.className = "icon-btn";
        deleteBtn.title = "Удалить подпапку";
        deleteBtn.textContent = "🗑";
        deleteBtn.addEventListener("click", (e) => {
          e.stopPropagation();
          deleteSubcategory(catName, subName);
        });

        actions.appendChild(editBtn);
        actions.appendChild(deleteBtn);

        item.appendChild(bullet);
        item.appendChild(label);
        item.appendChild(actions);

        item.addEventListener("click", () => {
          selectSubcategory(catName, subName);
        });

        subList.appendChild(item);
      });

      // строка "добавить подпапку"
      const addRow = document.createElement("div");
      addRow.className = "add-subcategory-row";
      const addLabel = document.createElement("span");
      addLabel.textContent = "Подпапки для этого раздела";
      const addRowBtn = document.createElement("button");
      addRowBtn.className = "icon-btn";
      addRowBtn.textContent = "+";
      addRowBtn.title = "Добавить новую подпапку";
      addRowBtn.addEventListener("click", (e) => {
        e.stopPropagation();
        addSubcategory(catName);
      });
      addRow.appendChild(addLabel);
      addRow.appendChild(addRowBtn);

      subList.appendChild(addRow);

      categoryEl.appendChild(header);
      categoryEl.appendChild(subList);

      sidebarContainer.appendChild(categoryEl);
    });
  }

  function addSubcategory(categoryName) {
    const label = prompt(`Название новой подпапки в разделе «${categoryName}»:`);
    if (!label) return;
    const trimmed = label.trim();
    if (!trimmed) return;

    if (!templateData[categoryName]) templateData[categoryName] = {};
    if (templateData[categoryName][trimmed]) {
      alert("Такая подпапка уже существует в этом разделе.");
      return;
    }

    templateData[categoryName][trimmed] = "";
    saveTemplateData();
    currentCategory = categoryName;
    currentSubcategory = trimmed;
    updateEditor();
    renderSidebar(searchInput.value);
  }

  function renameSubcategory(categoryName, subName) {
    const newName = prompt("Новое название подпапки:", subName);
    if (!newName || newName.trim() === subName) return;
    const trimmed = newName.trim();

    if (templateData[categoryName][trimmed]) {
      alert("Подпапка с таким названием уже есть.");
      return;
    }

    templateData[categoryName][trimmed] = templateData[categoryName][subName];
    delete templateData[categoryName][subName];
    saveTemplateData();

    if (currentCategory === categoryName && currentSubcategory === subName) {
      currentSubcategory = trimmed;
    }

    updateEditor();
    renderSidebar(searchInput.value);
  }

  function deleteSubcategory(categoryName, subName) {
    const confirmDelete = confirm(`Удалить подпапку «${subName}» и её текст?`);
    if (!confirmDelete) return;

    delete templateData[categoryName][subName];
    saveTemplateData();

    if (currentCategory === categoryName && currentSubcategory === subName) {
      currentCategory = null;
      currentSubcategory = null;
    }

    updateEditor();
    renderSidebar(searchInput.value);
  }

  function selectSubcategory(categoryName, subName) {
    currentCategory = categoryName;
    currentSubcategory = subName;
    updateEditor();
    renderSidebar(searchInput.value);
  }

  function updateEditor() {
    if (!currentCategory || !currentSubcategory) {
      templateTitle.textContent = "Выберите заготовку";
      templatePath.textContent = "Раздел / подпапка";
      templateText.value = "";
      templateText.disabled = true;
      saveTemplateBtn.disabled = true;
      currentTemplateHint.textContent = "Нет выбранной заготовки";
      return;
    }

    const text =
      (templateData[currentCategory] &&
        templateData[currentCategory][currentSubcategory]) ||
      "";

    templateTitle.textContent = currentSubcategory;
    templatePath.textContent = `${currentCategory} / ${currentSubcategory}`;
    templateText.disabled = false;
    templateText.value = text;
    saveTemplateBtn.disabled = false;
    currentTemplateHint.textContent = "Редактируйте текст и нажмите «Сохранить изменения».";
  }

  saveTemplateBtn.addEventListener("click", () => {
    if (!currentCategory || !currentSubcategory) return;
    const text = templateText.value;
    if (!templateData[currentCategory]) templateData[currentCategory] = {};
    templateData[currentCategory][currentSubcategory] = text;
    saveTemplateData();
    currentTemplateHint.textContent = "Сохранено.";
    setTimeout(() => {
      if (currentTemplateHint.textContent === "Сохранено.") {
        currentTemplateHint.textContent = "Редактируйте текст и нажмите «Сохранить изменения».";
      }
    }, 1500);
  });

  searchInput.addEventListener("input", () => {
    renderSidebar(searchInput.value);
  });

  // ====== INIT ======
  loadTemplateData();
  renderSidebar();
  updateEditor();
</script>
</body>
</html>

