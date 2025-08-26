File structure of vue components

If you find something else you can add it when you find it.

resources/
└── js/
    ├── Components/
    │   ├── Desktop/
    │   │   ├── Desktop.vue 			    # Main desktop canvas (#desktop-area). Hosts wallpaper, desktop icons, windows, drag selector, and acts as the "workspace".
    │   │   ├── AppLauncherMode.vue	  # Special launcher mode (like a quick app grid or alternative UI mode).
    │   │   ├── EasyMode.vue			    # Simplified desktop interface for less advanced users (like "tablet mode").
    │   │   ├── DesktopIcons.vue		  # Renders all app/shortcut icons on the desktop. Click = open window (via useWindows).
    │   │   ├── DragSelector.vue		  # Selection rectangle for multi-selecting icons (#drag-selector in HTML).
    │   │   ├── MobileDesktop.vue		  # Mobile-optimized version of the desktop (.mobile-profile-top-bar, .desktop-icons for mobile).
    │   │   └── MobileProfileBar.vue	# The mobile header with avatar, username, and search (from mobile profile top bar in index.html).
    │   │
    │   ├── Taskbar/
    │   │   ├── Taskbar.vue			      # Bottom bar that shows open apps, pinned apps, start menu button, and system tray.
    │   │   ├── TaskbarItem.vue		    # Represents a single app in the taskbar (open window, pinned icon). Controlled by useTaskbar.
    │   │   ├── SystemTray.vue			  # Tray area (notifications toggle, clock, audio icon, etc.).
    │   │   └── VolumePanel.vue		    # The full audio/music UI (#volume-panel in HTML). Includes player controls, playlist, and system volume slider.
    │   │
    │   ├── StartMenu/
    │   │   ├── StartMenu.vue			    # The full start menu (#start-menu). Combines left app grid and right sidebar.
    │   │   ├── StartMenuLeft.vue		  # Left panel of start menu, app grid (installed apps, categories).
    │   │   ├── StartMenuRight.vue		# Right sidebar (profile, website shortcuts, settings, etc.).
    │   │   └── StartMenuFooter.vue	  # Bottom bar of start menu (search input, logout button).
    │   │
    │   ├── Window/
    │   │   ├── Window.vue				    # Base draggable, resizable window. Uses composables for minimize/maximize/close (useWindows).
    │   │   ├── WindowHeader.vue		  # Title bar (app icon, title, controls). Supports maximize, minimize, popout, close.
    │   │   ├── WindowContent.vue		  # Slot wrapper for app UI inside a window.
    │   │   ├── WindowSidebar.vue		  # Sidebar panel inside apps (like File Explorer folders or Settings menu).
    │   │   └── WindowManager.vue		  # Manages all open windows (#windows-container). Iterates through useWindows store.
    │   │
    │   ├── Apps/					            # Preinstalled on the OS that cannot be uninstalled
    │   │   ├── FileExplorer			    # Folder to group apps if need it.
    │   │   │   ├── FileExplorer.vue	# Full app version of File Explorer (from <template id="file-explorer-template"> in index.html).
    │   │   │   └── WidgetsFileExplorer # Widget/minimized variant of File Explorer (for Widgets screen).
    │   │   ├── SettingsApp.vue		    # System settings app (<template id="settings-app-template">). Has side navigation, user profile, theme settings, etc.
    │   │   ├── SiteBuilderApp.vue		# Website/page builder (setupSiteBuilderApp in app.js). Manages site pages, SEO, publishing, and design settings.
    │   │   ├── AppStore.vue			    # App marketplace for installing/uninstalling optional apps.
    │   │   ├── Wallet.vue				    # Digital wallet app (payment methods, transactions, etc.).
    │   │   ├── EmailApp.vue			    # Email client (like from mailcow server with SOgo).
    │   │   ├── Calculator.vue			  # Simple calculator app.
    │   │   └── Calendar.vue			    # Full standalone calendar app.
    │   │
    │   ├── ContextMenu/
    │   │   ├── DesktopContextMenu.vue   # Desktop Context Meniu - right click
    │   │   ├── TaskbarContextMenu.vue		  # Task bar context menu
    │   │   ├── StartMenuContextMenu.vue 		  # Start Menu Context menu
    │   │   └── ......            		# Other context menues like apps, etc
    │   │    
    │   │   ├── Notifications/
    │   │   ├── NotificationsPanel.vue # Fullscreen panel for viewing all notifications (#notifications-screen).
    │   │   ├── Notification.vue		   # Single notification component (used in system tray or notifications panel).
    │   │   ├── SystemAlert.vue 		  # Alerts where you need to confirm or cancel like logout or uninstall app.
    │   │   └── ConfirmationNotification.vue		# Small notification on top of the window for confirmation, for example when a app in pinned or unpinned
    │   │
    │   ├── Widgets/
    │   │   └── WidgetsScreen.vue 		# Widgets dashboard (#widgets-screen). Hosts calendar, weather, music, etc.
    │   │
    │   └── Layouts/
    │       ├── OSLayout.vue			    # Root layout combining Desktop, Taskbar, StartMenu, Notifications, and Widgets. The “OS shell”.
    │       ├── MobileOSLayout.vue		# Root layout for mobile version.
    │       └── TabletOSLayout.vue		# Root layout combining Desktop, Taskbar, StartMenu, Notifications, and Widgets. The “OS shell”.
    │
    ├── Composables/
    │   ├── useWindows.ts        		   # All window lifecycle State & logic for windows (open/close/minimize/popout)
    │   ├── useTaskbar.ts        		   # Taskbar behavior (pin/unpin apps, update active taskbar item, sync with useWindows)
    │   ├── useStartMenu.ts      		   # Start menu state (open/close start menu, search/filter apps, handle keyboard shortcut)
    │   ├── useVolume.ts         		   # Music/volume panel state
    │   └── useNotifications.ts  	     # Notification handling (push new notifications, toggle notifications panel, stack mode (one, three, all))
    │
    ├── Stores/                  		   # Pinia stores (all in TS)
    │   ├── windows.ts					      # State for open windows, active window, window positions.
    │   ├── apps.ts					          # Registry of apps (id, name, icon, Vue component). Handles app launching & pinned apps.
    │   ├── settings.ts				        # Global OS settings: wallpaper, theme, language, desktop modes (easy/advanced).
    │   └── audio.ts					        # Music player + system volume state.
    │
    ├── Types/                  		  # Global TS types/interfaces
    │   ├── window.d.ts          		  # Window state (id, title, icon, position, size, flags for active/minimized/maximized).
    │   ├── app.d.ts             		  # App metadata (id, name, icon, component, pinned flag).
    │   ├── notifications.d.ts   		  # Notification interface (id, message, type, createdAt).
    │   └── audio.d.ts           		  # Audio/volume state (muted, volume, current track, playlist).
    │
    └── Pages/
        └── Dashboard.vue				      # Main Inertia/Vue entry point for the OS dashboard. Mounts OSLayout.vue.
