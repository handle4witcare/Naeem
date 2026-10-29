<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no" />
  <meta name="theme-color" content="#0f0f13" />
  <meta name="description" content="Naeem — Create, build and animate movies & scenes with AI-powered storyboarding and prompt generation." />
  <title>Naeem — AI Movie & Scene Studio</title>
  <link rel="stylesheet" href="css/styles.css" />
  <link rel="preconnect" href="https://fonts.googleapis.com" />
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&family=JetBrains+Mono:wght@400;500&display=swap" rel="stylesheet" />
</head>
<body>
  <div id="app">
    <!-- Top Navigation -->
    <header class="topbar">
      <div class="brand" onclick="App.showView('home')">
        <div class="logo">N</div>
        <span class="brand-name">Naeem <span class="ai-badge">AI</span></span>
      </div>
      <nav class="nav-links" id="main-nav">
        <button class="nav-btn active" data-view="home">Home</button>
        <button class="nav-btn" data-view="studio" id="nav-studio" style="display:none">Studio</button>
        <button class="nav-btn" data-view="library">Library</button>
      </nav>
      <div class="topbar-actions">
        <button class="icon-btn" id="security-btn" title="Security & encryption" onclick="App.openSecurityModal()">🔒</button>
        <button class="icon-btn" id="theme-toggle" title="Toggle theme">◐</button>
        <button class="btn btn-primary" id="new-project-btn">+ New Project</button>
      </div>
    </header>

    <!-- Main Content Area -->
    <main id="main-content">
      <!-- HOME VIEW -->
      <section id="view-home" class="view active">
        <div class="hero">
          <h1>Create movies & scenes<br><span class="gradient-text">with AI</span></h1>
          <p class="hero-sub">From idea → script → storyboard → animation-ready prompts.<br>Build complete short films in your browser.</p>
          <div class="hero-actions">
            <button class="btn btn-primary btn-lg" onclick="App.createProject()">Start Creating</button>
            <button class="btn btn-ghost btn-lg" onclick="App.showView('library')">Open Library</button>
          </div>
        </div>

        <div class="features-grid">
          <div class="feature-card">
            <div class="feature-icon">📝</div>
            <h3>AI Script & Outline</h3>
            <p>Describe your idea. Naeem expands it into scenes, beats, and dialogue suggestions.</p>
          </div>
          <div class="feature-card">
            <div class="feature-icon">🎬</div>
            <h3>Storyboard Builder</h3>
            <p>Organize shots, set durations, camera moves, and generate precise prompts for every frame.</p>
          </div>
          <div class="feature-card">
            <div class="feature-icon">👤</div>
            <h3>Character Consistency</h3>
            <p>Define characters once. Reuse them across scenes so AI tools keep appearance consistent.</p>
          </div>
          <div class="feature-card">
            <div class="feature-icon">⚡</div>
            <h3>Prompt Export</h3>
            <p>One-click prompts optimized for Kling, Runway, Seedance, Dreamina, Pika, Veo and more.</p>
          </div>
        </div>

        <div class="how-it-works">
          <h2>How it works</h2>
          <div class="steps">
            <div class="step">
              <span class="step-num">1</span>
              <h4>Idea</h4>
              <p>Write a short description or paste a script.</p>
            </div>
            <div class="step">
              <span class="step-num">2</span>
              <h4>Structure</h4>
              <p>AI breaks it into scenes, characters and shot list.</p>
            </div>
            <div class="step">
              <span class="step-num">3</span>
              <h4>Refine</h4>
              <p>Edit prompts, add camera notes, set timing.</p>
            </div>
            <div class="step">
              <span class="step-num">4</span>
              <h4>Generate</h4>
              <p>Copy prompts into your favorite AI video tool and assemble.</p>
            </div>
          </div>
        </div>
      </section>

      <!-- LIBRARY VIEW -->
      <section id="view-library" class="view">
        <div class="section-header">
          <h2>Your Projects</h2>
          <button class="btn btn-primary" onclick="App.createProject()">+ New Project</button>
        </div>
        <div id="project-list" class="project-grid">
          <!-- filled by JS -->
        </div>
        <div id="empty-library" class="empty-state" style="display:none">
          <p>No projects yet.</p>
          <button class="btn btn-primary" onclick="App.createProject()">Create your first movie</button>
        </div>
      </section>

      <!-- STUDIO VIEW -->
      <section id="view-studio" class="view">
        <div class="studio-layout">
          <!-- Left sidebar: project meta + characters -->
          <aside class="studio-sidebar">
            <div class="sidebar-section">
              <label class="label">Project Title</label>
              <input type="text" id="project-title" class="input" placeholder="Untitled Film" />
            </div>
            <div class="sidebar-section">
              <label class="label">Genre / Style</label>
              <select id="project-style" class="input">
                <option value="cinematic">Cinematic / Photoreal</option>
                <option value="pixar">3D Pixar-style</option>
                <option value="anime">Anime</option>
                <option value="2d">2D Flat / Cartoon</option>
                <option value="noir">Film Noir</option>
                <option value="fantasy">Fantasy Epic</option>
                <option value="scifi">Sci-Fi</option>
                <option value="documentary">Documentary</option>
              </select>
            </div>
            <div class="sidebar-section">
              <label class="label">Aspect Ratio</label>
              <select id="project-aspect" class="input">
                <option value="16:9">16:9 Landscape</option>
                <option value="9:16">9:16 Vertical</option>
                <option value="1:1">1:1 Square</option>
                <option value="2.39:1">2.39:1 Cinemascope</option>
              </select>
            </div>

            <div class="sidebar-section">
              <div class="section-row">
                <label class="label">Characters</label>
                <button class="btn-sm" onclick="App.addCharacter()">+</button>
              </div>
              <div id="character-list" class="char-list"></div>
            </div>

            <div class="sidebar-actions">
              <button class="btn btn-ghost btn-block" onclick="App.saveProject()">Save Project</button>
              <button class="btn btn-primary btn-block" onclick="App.exportProject()">Export All</button>
            </div>
          </aside>

          <!-- Center: main workspace -->
          <div class="studio-main">
            <div class="studio-tabs">
              <button class="tab active" data-tab="idea">Idea & Script</button>
              <button class="tab" data-tab="storyboard">Storyboard</button>
              <button class="tab" data-tab="timeline">Timeline</button>
              <button class="tab" data-tab="prompts">Prompts</button>
              <button class="tab" data-tab="preview">Preview</button>
              <button class="tab" data-tab="download">Download</button>
            </div>

            <!-- TAB: IDEA -->
            <div id="tab-idea" class="tab-panel active">
              <div class="panel-header">
                <h3>Describe your movie or scene</h3>
                <p class="muted">Write a short synopsis, a full script, or just a vibe. Then let AI structure it.</p>
              </div>
              <textarea id="idea-input" class="textarea large" placeholder="Example: A lonely robot gardener discovers a single flower growing in a ruined city. Over three days it learns to protect the flower from acid rain and finally finds a community of other robots who help it plant a garden. Warm, hopeful, Pixar-style, no dialogue, 45 seconds."></textarea>
              <div class="panel-actions">
                <button class="btn btn-primary" id="generate-structure-btn" onclick="App.generateStructure()">
                  <span class="btn-text">Generate Structure with AI</span>
                  <span class="btn-loader" style="display:none">Generating…</span>
                </button>
              </div>
              <div id="script-preview" class="script-preview" style="display:none">
                <h4>Generated Outline</h4>
                <div id="script-content"></div>
              </div>
            </div>

            <!-- TAB: STORYBOARD -->
            <div id="tab-storyboard" class="tab-panel">
              <div class="panel-header row">
                <div>
                  <h3>Storyboard</h3>
                  <p class="muted">Each card is a shot. Edit description, camera, and AI prompt.</p>
                </div>
                <button class="btn btn-primary" onclick="App.addShot()">+ Add Shot</button>
              </div>
              <div id="storyboard-list" class="storyboard-list"></div>
            </div>

            <!-- TAB: TIMELINE -->
            <div id="tab-timeline" class="tab-panel">
              <div class="panel-header">
                <h3>Timeline</h3>
                <p class="muted">Drag to reorder. Hard limit: 15 minutes total. Duration updates automatically.</p>
              </div>
              <div class="timeline-header">
                <span id="total-duration">0s <span class="limit-label">/ 15 min max</span></span>
              </div>
              <div id="timeline-track" class="timeline-track"></div>
            </div>

            <!-- TAB: PROMPTS -->
            <div id="tab-prompts" class="tab-panel">
              <div class="panel-header">
                <h3>Ready-to-use AI Prompts</h3>
                <p class="muted">Copy these into Kling, Runway, Seedance, Dreamina, Pika, Veo, etc.</p>
              </div>
              <div class="prompt-tools">
                <label>Target model style</label>
                <select id="prompt-model" class="input" onchange="App.refreshPrompts()">
                  <option value="general">General / Universal</option>
                  <option value="kling">Kling AI</option>
                  <option value="runway">Runway</option>
                  <option value="seedance">Seedance / Dreamina</option>
                  <option value="pika">Pika</option>
                  <option value="veo">Google Veo</option>
                </select>
              </div>
              <div id="prompt-list" class="prompt-list"></div>
            </div>

            <!-- TAB: PREVIEW -->
            <div id="tab-preview" class="tab-panel">
              <div class="panel-header">
                <h3>Project Preview</h3>
                <p class="muted">Play through your shots in sequence. This is a timed storyboard preview (not rendered video).</p>
              </div>
              <div class="preview-player">
                <div class="preview-screen" id="preview-screen">
                  <div class="preview-placeholder" id="preview-placeholder">
                    <p>Press Play to preview your project</p>
                  </div>
                  <div class="preview-content" id="preview-content" style="display:none">
                    <div class="preview-shot-num" id="preview-shot-num"></div>
                    <h2 class="preview-title" id="preview-title"></h2>
                    <p class="preview-desc" id="preview-desc"></p>
                    <p class="preview-camera" id="preview-camera"></p>
                  </div>
                </div>
                <div class="preview-controls">
                  <button class="btn btn-ghost" id="preview-prev" onclick="App.previewPrev()" disabled>◀ Prev</button>
                  <button class="btn btn-primary" id="preview-play" onclick="App.togglePreview()">▶ Play</button>
                  <button class="btn btn-ghost" id="preview-next" onclick="App.previewNext()" disabled>Next ▶</button>
                </div>
                <div class="preview-progress-wrap">
                  <div class="preview-progress-bar" id="preview-progress-bar"></div>
                </div>
                <div class="preview-meta">
                  <span id="preview-time">0:00 / 0:00</span>
                  <span id="preview-shot-info">Shot 0 of 0</span>
                </div>
              </div>
            </div>

            <!-- TAB: DOWNLOAD -->
            <div id="tab-download" class="tab-panel">
              <div class="panel-header">
                <h3>Download your project</h3>
                <p class="muted">Export everything you need to generate video with external AI tools or keep a backup.</p>
              </div>
              <div class="download-grid">
                <div class="download-card">
                  <h4>📦 Full Project (JSON)</h4>
                  <p class="muted">Complete project data — idea, characters, shots, prompts. Re-import later or share.</p>
                  <button class="btn btn-primary" onclick="App.downloadJSON()">Download JSON</button>
                </div>
                <div class="download-card">
                  <h4>📝 All Prompts (TXT)</h4>
                  <p class="muted">Ready-to-paste prompts for every shot, tuned to the selected model style.</p>
                  <button class="btn btn-primary" onclick="App.downloadPrompts()">Download Prompts</button>
                </div>
                <div class="download-card">
                  <h4>🎬 Storyboard (HTML)</h4>
                  <p class="muted">Printable / shareable storyboard page you can open in any browser or print to PDF.</p>
                  <button class="btn btn-primary" onclick="App.downloadStoryboard()">Download Storyboard</button>
                </div>
                <div class="download-card">
                  <h4>📋 Shot List (CSV)</h4>
                  <p class="muted">Spreadsheet-friendly list of shots, durations, cameras, and descriptions.</p>
                  <button class="btn btn-primary" onclick="App.downloadCSV()">Download CSV</button>
                </div>
              </div>
            </div>
          </div>
        </div>
      </section>
    </main>

    <!-- Modal: Character Editor -->
    <div id="modal-character" class="modal" style="display:none">
      <div class="modal-content">
        <div class="modal-header">
          <h3 id="char-modal-title">Add Character</h3>
          <button class="icon-btn" onclick="App.closeModal()">×</button>
        </div>
        <div class="modal-body">
          <label class="label">Name</label>
          <input type="text" id="char-name" class="input" placeholder="e.g. Luna the Robot" />
          <label class="label">Appearance description</label>
          <textarea id="char-desc" class="textarea" placeholder="Small white robot with glowing blue eyes, rusty joints, gentle posture..."></textarea>
          <label class="label">Personality / Role</label>
          <input type="text" id="char-role" class="input" placeholder="Curious, protective, silent" />
        </div>
        <div class="modal-footer">
          <button class="btn btn-ghost" onclick="App.closeModal()">Cancel</button>
          <button class="btn btn-primary" id="save-char-btn" onclick="App.saveCharacter()">Save Character</button>
        </div>
      </div>
    </div>

    <!-- Modal: Security / Encryption -->
    <div id="modal-security" class="modal" style="display:none">
      <div class="modal-content">
        <div class="modal-header">
          <h3>Security & Encryption</h3>
          <button class="icon-btn" onclick="App.closeSecurityModal()">×</button>
        </div>
        <div class="modal-body">
          <p class="muted" style="font-size:0.85rem;margin-bottom:0.8rem">
            Projects can be encrypted with AES-256-GCM. Keys are derived from your passphrase via PBKDF2 (250k iterations) and never stored. A fresh random IV is used on every save so ciphertext changes frequently.
          </p>
          <div id="sec-status" class="muted" style="margin-bottom:0.8rem;font-size:0.85rem"></div>

          <div id="sec-enable-panel">
            <label class="label">Set passphrase (min 8 chars)</label>
            <input type="password" id="sec-pass" class="input" placeholder="Choose a strong passphrase" autocomplete="new-password" />
            <label class="label" style="margin-top:0.6rem">Confirm passphrase</label>
            <input type="password" id="sec-pass-confirm" class="input" placeholder="Confirm" autocomplete="new-password" />
          </div>

          <div id="sec-unlock-panel" style="display:none">
            <label class="label">Enter passphrase to unlock</label>
            <input type="password" id="sec-unlock-pass" class="input" placeholder="Passphrase" autocomplete="current-password" />
          </div>

          <div id="sec-change-panel" style="display:none">
            <label class="label">Current passphrase</label>
            <input type="password" id="sec-old-pass" class="input" placeholder="Current" autocomplete="current-password" />
            <label class="label" style="margin-top:0.6rem">New passphrase</label>
            <input type="password" id="sec-new-pass" class="input" placeholder="New (min 8 chars)" autocomplete="new-password" />
          </div>
        </div>
        <div class="modal-footer">
          <button class="btn btn-ghost" onclick="App.closeSecurityModal()">Close</button>
          <button class="btn btn-primary" id="sec-action-btn" onclick="App.handleSecurityAction()">Enable Encryption</button>
        </div>
      </div>
    </div>

    <!-- Toast -->
    <div id="toast" class="toast" style="display:none"></div>
  </div>

  <script src="js/app.js"></script>
</body>
</html>
