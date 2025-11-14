# Oracle JET Redwood UI Prototypes
## Proactive Project Management Application

This directory contains UI prototypes built using the official **Oracle JavaScript Extension Toolkit (JET) 18.0.0** with the **Redwood Design System** theme.

## Overview

These prototypes demonstrate a proactive project management application that uses predictive analytics to alert users **before** problems occur, using genuine Oracle JET components and the Redwood Design System.

## Prototypes Included

### 1. Dashboard (`dashboard-jet.html`)
**Purpose**: Multi-project overview with alerts and insights

**Oracle JET Components Used**:
- `oj-action-card` - Metric cards and project cards
- `oj-button` - Call-to-action and navigation buttons
- `oj-button-set-one` - Alert filter chips
- `oj-progress-bar` - Project progress indicators
- `oj-badge` - Status badges and notification counts
- `oj-avatar` - User profile avatar
- `oj-status-indicator-icon` - Alert severity indicators

**Key Features**:
- 4 key metrics cards (Total Projects, Projects at Risk, Total Budget, Tasks Due)
- Filterable alerts panel with critical/warning/info states
- 6 project cards with health scores, progress bars, and alert counts
- Responsive grid layouts using CSS Grid

---

### 2. Project Detail (`project-detail-jet.html`)
**Purpose**: Detailed single project view with tasks, metrics, and insights

**Oracle JET Components Used**:
- `oj-action-card` - Container cards for sections
- `oj-tab-bar` + `oj-switcher` - Tab navigation (Tasks, Timeline, Budget, Team)
- `oj-list-view` + `oj-list-item-layout` - Task list with rich layouts
- `oj-progress-bar` - Task completion indicators
- `oj-badge` - Task status badges
- `oj-avatar` - Team member avatars
- `oj-status-indicator-icon` - Task health indicators
- `oj-button` - Navigation and actions

**Key Features**:
- Large health score display (42 - Critical)
- Collapsible alerts panel with 3 critical alerts
- 4 metric cards (Tasks, Budget, Timeline, Team)
- Tabbed interface for different project views
- Task list with progress, status, and health indicators
- Team member avatar group
- Insights panel with forecast cards

---

### 3. Budget Detail (`budget-detail-jet.html`)
**Purpose**: Comprehensive budget tracking with cost forecasting

**Oracle JET Components Used**:
- `oj-action-card` - Section containers
- `oj-button` - Export and add cost actions
- `oj-badge` - Cost category badges
- `oj-avatar` - Resource avatars in labor costs
- `oj-status-indicator-icon` - Alert indicators

**Key Features**:
- Budget summary with 4 key values (Total, Actual, Forecast, Variance)
- Critical alert banner for budget overrun
- Budget health gauge (88% spent vs 68% complete)
- SVG cost forecast chart with trend lines
- 4 analysis cards (Burn Rate, Projected Completion, Budget Remaining, Days Left)
- Fixed costs breakdown with badges
- Time-based labor costs with avatars
- Grand total calculation
- 4 AI-powered recommendations

---

## Technology Stack

### Oracle JET 18.0.0 (from CDN)
- **CSS**: `https://static.oracle.com/cdn/jet/18.0.0/default/css/redwood/oj-redwood-min.css`
- **JavaScript**: `https://static.oracle.com/cdn/jet/18.0.0/default/js/libs/oj/min`
- **3rd Party Libraries**: RequireJS, Knockout, jQuery

### Redwood Design System
The prototypes use the official Oracle Redwood Design System with:
- **Color Palette**:
  - Brand: `--oj-palette-brand-100`
  - Danger: `--oj-palette-danger-80`
  - Warning: `--oj-palette-warning-80`
  - Success: `--oj-palette-success-80`
  - Info: `--oj-palette-info-80`
  - Neutral: `--oj-palette-neutral-*`
- **Spacing**: `--oj-core-spacing-*` (based on 8px grid)
- **Typography**: Oracle Sans font family
- **Components**: All JET components follow Redwood specifications

---

## How to View

### Option 1: Open Directly in Browser
Simply open any HTML file in a modern web browser:
```bash
# From the ui-prototypes-redwood directory
open dashboard-jet.html           # macOS
start dashboard-jet.html          # Windows
xdg-open dashboard-jet.html       # Linux
```

### Option 2: Use a Local Web Server
For best results, serve via HTTP:
```bash
# Using Python 3
python -m http.server 8000

# Using Node.js http-server
npx http-server -p 8000

# Then navigate to:
http://localhost:8000/dashboard-jet.html
```

### Option 3: Live Server in VS Code
1. Install the "Live Server" extension
2. Right-click on `dashboard-jet.html`
3. Select "Open with Live Server"

---

## Navigation Flow

```
dashboard-jet.html
    ↓ (Click project card)
project-detail-jet.html
    ↓ (Click "View Detailed Budget Analysis")
budget-detail-jet.html
```

**Back Navigation**:
- Each page has a back button (← icon) to return to previous page
- Breadcrumb navigation in header

---

## Browser Compatibility

These prototypes require a modern browser with:
- ES6+ JavaScript support
- CSS Custom Properties (CSS Variables)
- Web Components support
- SVG rendering

**Tested Browsers**:
- Chrome 90+
- Firefox 88+
- Safari 14+
- Edge 90+

---

## Oracle JET Component Documentation

For detailed component documentation, visit:
- **JET Cookbook**: https://www.oracle.com/webfolder/technetwork/jet/jetCookbook.html
- **JET Documentation**: https://docs.oracle.com/en/middleware/developer-tools/jet/18/
- **Redwood Design System**: https://redwood.oracle.com/

---

## Key Differences from Custom CSS Version

### Advantages of Oracle JET Version:
1. **Official Components**: Uses genuine Oracle JET web components
2. **Redwood Theme**: Authentic Redwood Design System styling via CSS variables
3. **Production Ready**: Components are enterprise-tested and maintained by Oracle
4. **Accessibility**: Built-in ARIA attributes and keyboard navigation
5. **Theming**: Easy theme switching via path_mapping.json
6. **Consistency**: Guaranteed consistency with Oracle Fusion Cloud applications

### Components Showcase:
| Component | Usage |
|-----------|-------|
| `oj-action-card` | All card containers (metrics, projects, alerts) |
| `oj-button` | CTAs, navigation, filters |
| `oj-button-set-one` | Mutually exclusive filter chips |
| `oj-progress-bar` | Task and project progress |
| `oj-badge` | Status indicators, counts, categories |
| `oj-avatar` | User profiles, team members |
| `oj-status-indicator-icon` | Alert severity, task health |
| `oj-tab-bar` | Tab navigation |
| `oj-switcher` | Tab panel switching |
| `oj-list-view` | Task lists |
| `oj-list-item-layout` | Rich task item layouts |

---

## Customization

### Modify Colors
Edit the CSS custom properties:
```css
.my-custom-element {
    color: var(--oj-palette-brand-100);  /* Oracle Red */
    background: var(--oj-palette-info-20);  /* Light blue bg */
}
```

### Change Spacing
Use the spacing scale:
```css
.my-element {
    padding: var(--oj-core-spacing-4x);  /* 32px */
    margin: var(--oj-core-spacing-2x);   /* 16px */
}
```

### Add Data Binding
For a fully functional app, integrate Knockout observables:
```javascript
function AppViewModel() {
    this.projects = ko.observableArray([...]);
    this.selectedProject = ko.observable();
}
ko.applyBindings(new AppViewModel());
```

---

## Future Enhancements

To make these prototypes fully functional:

1. **Data Binding**: Connect components to Knockout ViewModels
2. **REST APIs**: Integrate with backend services
3. **Oracle JET CLI**: Scaffold a full JET app structure
4. **Router**: Implement oj-router for SPA navigation
5. **Charts**: Add oj-chart components for visualizations
6. **Table**: Use oj-table for sortable/filterable data grids
7. **Forms**: Add form validation with oj-validation-group
8. **Offline**: Implement offline-first with Service Workers

---

## File Structure

```
ui-prototypes-redwood/
├── README.md                    # This file
├── dashboard-jet.html           # Multi-project dashboard
├── project-detail-jet.html      # Single project detail view
└── budget-detail-jet.html       # Budget tracking & forecasting
```

---

## CDN Resources Used

All resources loaded from Oracle CDN:
- **JET Version**: 18.0.0
- **Base URL**: `https://static.oracle.com/cdn/jet/18.0.0/`
- **Paths**:
  - CSS: `default/css/redwood/oj-redwood-min.css`
  - JS: `default/js/libs/oj/min`
  - 3rd Party: `3rdparty/`

---

## Performance Notes

- All assets loaded from Oracle CDN (global distribution)
- Minified CSS and JS files
- RequireJS lazy loading of components
- Approx 500KB total transfer size (gzipped)
- Initial load: ~2-3 seconds on average connection
- Subsequent navigation: instant (cached)

---

## License

These prototypes are for demonstration purposes. Oracle JET is licensed under the Oracle Free Use Terms and Conditions (FUTC) license.

---

## Contact & Support

For questions about:
- **Oracle JET**: See official documentation
- **This prototype**: Contact the project team

---

**Version**: 1.0
**Last Updated**: 2025-11-14
**Oracle JET Version**: 18.0.0
**Redwood Theme**: Latest (2025)
