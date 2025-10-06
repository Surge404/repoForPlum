# AI-Powered Benefits Discovery Flow

A beautiful, interactive React web application that uses AI to help users discover and understand their benefits. Built with React, Tailwind CSS, Recoil, Framer Motion, and Google Gemini AI.

## Features

- **Intelligent Classification**: AI-powered text analysis to categorize user queries into Dental, OPD, Vision, or Mental Health benefits
- **Dynamic Benefit Matching**: Automatically matches user needs with relevant benefits
- **Personalized Action Plans**: AI-generated 3-step action plans for each benefit
- **Stunning Animations**: Smooth transitions, floating elements, and engaging micro-interactions using Framer Motion
- **Dark Mode**: Seamless dark/light theme toggle with beautiful gradients
- **Responsive Design**: Fully responsive layout that works on all devices
- **Modern UI/UX**: Creative, non-traditional design with glassmorphism effects and gradient backgrounds

## Tech Stack

- **React 18** - UI framework
- **Tailwind CSS** - Utility-first styling
- **Recoil** - State management
- **Framer Motion** - Advanced animations
- **Google Gemini AI** - AI classification and generation
- **Vite** - Build tool and dev server
- **Lucide React** - Beautiful icons

## Quick Start

### Prerequisites

- Node.js 16+ and npm

### Installation & Running

```bash
# Install dependencies
npm install

# Start development server
npm start

# Build for production
npm run build

# Preview production build
npm run preview
```

The app will be available at `http://localhost:5173`

## Project Structure

```
src/
├── components/          # React components
│   ├── BenefitInput.jsx       # Initial input screen
│   ├── ProcessingScreen.jsx   # Loading/classification screen
│   ├── BenefitList.jsx        # Benefits listing screen
│   ├── BenefitCard.jsx        # Individual benefit card
│   └── BenefitDetails.jsx     # Benefit details & action plan
├── data/
│   └── benefits.mock.json     # Mock benefits data
├── services/
│   └── aiService.js           # AI integration service
├── state/
│   └── atoms.js               # Recoil state management
├── App.jsx                    # Main app component
├── main.jsx                   # App entry point
└── index.css                  # Global styles & animations
```

## AI Integration

This app uses **Google Gemini AI** for intelligent text processing. The AI handles three main tasks:

### 1. Classification Prompt

Classifies user input into one of four benefit categories:

```
Return ONLY one of these category names — Dental, OPD, Vision, Mental Health — that best matches the user text. Output exactly the category name and nothing else. If the text is ambiguous or none match, output "UNRECOGNIZED".

User text: "{user_input}"
```

**Expected Output**: `Dental` | `OPD` | `Vision` | `Mental Health` | `UNRECOGNIZED`

### 2. Clarification Prompt

Used when classification is ambiguous:

```
The user wrote: "{user_input}". Ask a single concise clarifying question that will help classify this into Dental, OPD, Vision, or Mental Health. Return ONLY the clarifying question sentence.
```

**Expected Output**: A single clarifying question string

### 3. Action Plan Prompt

Generates a structured 3-step action plan:

```
Given:

selectedBenefit: {
  title: "{benefit.title}",
  coverage: {benefit.coverage}%,
  description: "{benefit.description}"
}
user_input: "{user_input}"

Return a JSON object exactly in this shape (no extra text):
{
  "steps": [
    {
      "step": 1,
      "title": "Short title (max 6 words)",
      "description": "Action description (1-2 sentences).",
      "estimatedTime": "e.g. 1-2 days or 1 hour",
      "requiredDocs": ["list","of","docs"]
    },
    {
      "step": 2,
      "title": "...",
      "description": "...",
      "estimatedTime": "...",
      "requiredDocs": [...]
    },
    {
      "step": 3,
      "title": "...",
      "description": "...",
      "estimatedTime": "...",
      "requiredDocs": [...]
    }
  ],
  "notes": "One-sentence extra note if needed, otherwise empty string"
}
```

**Expected Output**: Strict JSON object with steps array and notes

## API Configuration

The Gemini API key is configured in `src/services/aiService.js`:

```javascript
const GEMINI_API_KEY = 'AIzaSyDuMnKNw3dqnURwgBWOx8Gs0UgVx9qdM64';
const GEMINI_API_URL = 'https://generativelanguage.googleapis.com/v1beta/models/gemini-pro:generateContent';
```

To use your own API key:

1. Get an API key from [Google AI Studio](https://makersuite.google.com/app/apikey)
2. Replace the `GEMINI_API_KEY` value in `src/services/aiService.js`

## User Flow

1. **Input Screen**: User enters their health concern (e.g., "I have tooth pain, what can I do?")
2. **Processing Screen**: Beautiful loading animation while AI classifies the request
3. **Benefits List**: 2-6 relevant benefit cards displayed based on classification
4. **Benefit Details**: User selects a benefit to view AI-generated 3-step action plan

### Features in Each Screen

**Input Screen**:
- Free-text input with friendly placeholder
- Example queries for quick testing
- Animated gradient background
- Feature highlights

**Processing Screen**:
- Animated rotating rings
- Pulsing brain icon
- Orbiting sparkles
- Status indicators
- User query display

**Benefits List**:
- Animated benefit cards with hover effects
- Coverage percentage badges
- Category tags
- Regenerate functionality
- Back navigation

**Benefit Details**:
- Full benefit overview
- AI-generated 3-step action plan
- Expandable steps with required documents
- Time estimates for each step
- Additional notes
- Regenerate action plan option

## Mock Data

The app includes 6 mock benefits across 4 categories:

- **Dental**: Cleaning & Checkup (80%), Tooth Extraction (70%), Root Canal (65%)
- **Mental Health**: Counseling (90%)
- **Vision**: Eye Exam (50%)
- **OPD**: General Consultation (75%)

Benefits are stored in `src/data/benefits.mock.json` and can be easily modified.

## State Management

The app uses Recoil for state management with the following atoms:

- `userInputState` - Current user input
- `classificationState` - AI classification result
- `selectedBenefitState` - Currently selected benefit
- `actionPlanState` - Generated action plan
- `currentScreenState` - Active screen (input/processing/benefits/details)
- `darkModeState` - Dark mode toggle
- `isClassifyingState` - Loading state for classification
- `isGeneratingPlanState` - Loading state for action plan generation

## Customization

### Adding New Benefits

Edit `src/data/benefits.mock.json`:

```json
{
  "id": "unique-id",
  "category": "Dental|OPD|Vision|Mental Health",
  "title": "Benefit Title",
  "coverage": 80,
  "description": "Benefit description",
  "icon": "🦷",
  "color": "from-cyan-500 to-blue-600"
}
```

### Changing Colors

All gradients use Tailwind CSS classes. Update the `color` field in benefits or modify component gradient classes.

### Modifying Animations

Animations are defined in components using Framer Motion. Key animation files:
- `src/components/BenefitInput.jsx` - Floating background blobs
- `src/components/ProcessingScreen.jsx` - Rotating rings and orbiting elements
- `src/components/BenefitCard.jsx` - Card hover effects
- `src/index.css` - Custom CSS animations

## Assumptions & Limitations

- The app currently uses a real AI API (Google Gemini) but includes mock benefits data
- No backend or database - all data is client-side
- No user authentication
- No benefit claiming/application process
- Classification is limited to 4 predefined categories
- Action plans are AI-generated and may vary in quality

## Known Issues

- AI responses may occasionally not follow exact format (handled with error catching)
- No retry limit on API calls
- Dark mode preference not persisted across sessions
- No analytics or usage tracking

## Next Steps & Future Enhancements

1. **Backend Integration**:
   - User authentication
   - Benefit application workflow
   - Save user history and action plans

2. **Enhanced AI**:
   - Multi-turn conversations
   - Context-aware follow-up questions
   - Learning from user feedback

3. **Extended Features**:
   - Calendar integration for appointments
   - Document upload and management
   - Provider search and directory
   - Cost estimation tools
   - Claims tracking

4. **Accessibility**:
   - Screen reader optimization
   - Keyboard navigation improvements
   - ARIA labels enhancement
   - High contrast mode

5. **Performance**:
   - Code splitting
   - Image optimization
   - Caching strategies
   - Progressive Web App (PWA)

## Testing

To test the AI classification, try these queries:

- **Dental**: "I have tooth pain", "Need dental cleaning", "Cavity treatment"
- **Vision**: "Blurry vision", "Need glasses", "Eye exam"
- **Mental Health**: "Feeling anxious", "Depression support", "Therapy sessions"
- **OPD**: "General checkup", "Fever and cold", "Medical consultation"

## Accessibility

The app includes:

- Semantic HTML elements
- ARIA labels on interactive elements
- Keyboard navigation support
- Focus indicators
- Sufficient color contrast ratios
- Screen reader friendly content

## Browser Support

- Chrome (latest)
- Firefox (latest)
- Safari (latest)
- Edge (latest)

## License

This is a demonstration project. Feel free to use and modify as needed.

## Credits

- Built with ❤️ using React and modern web technologies
- Icons by [Lucide](https://lucide.dev)
- AI powered by [Google Gemini](https://ai.google.dev)

---

**Note**: This is a frontend demonstration project. In production, API keys should be stored securely on the backend, and all AI calls should be proxied through your own server for security and rate limiting.
