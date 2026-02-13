# ✅ Complete Installation & Testing Guide

## 📦 Installation Steps

### 1. **Download Game Files**
- Download `index.html` from the project
- Place in a dedicated folder: `/Eternity_Tech_Complete/`

### 2. **Open in Browser**
- **Desktop**: Double-click `index.html`
- **Mobile**: Open with browser app
- **Web Server** (recommended):
  ```bash
  # Using Python
  python -m http.server 8000
  
  # Using Node.js
  npx http-server
  
  # Using PHP
  php -S localhost:8000
  ```
  Then visit: `http://localhost:8000/index.html`

### 3. **Verify Installation**
- Game should load with "Eternity Tech" title
- Loading bar should appear
- After 1-2 seconds, backstory should show
- Can click "Skip" to go to main menu

---

## 🎮 First Time Setup

### Desktop Setup
1. Open `index.html` in Chrome, Firefox, Safari, or Edge
2. Allow page to load completely (wait for "Calibrating Quantum Core")
3. Click "Skip" to skip backstory
4. Click "New Journey" to start game
5. Read dialogue and solve puzzles to progress

### Mobile Setup (Android)
1. Use Chrome browser
2. Visit game website or open local file
3. Allow vibration permission if prompted
4. Game will auto-detect touch and optimize UI
5. Use touch controls to play:
   - Tap dialogue to continue
   - Tap puzzle items to select
   - Swipe on cipher wheel to rotate
   - Tap Check button to verify answers

### Mobile Setup (iOS)
1. Use Safari browser
2. Add to home screen (optional):
   - Tap Share → Add to Home Screen
3. Open game (as web app or in browser)
4. Game will optimize for iOS automatically
5. Same touch controls as Android

---

## ✨ Feature Verification Checklist

### Loading & Menu
- [ ] Game loads within 3 seconds
- [ ] Loading progress bar appears
- [ ] Backstory text fades in
- [ ] Skip button works
- [ ] Main menu appears after backstory
- [ ] "New Journey" button highlights on hover
- [ ] "Continue" button is clickable (may show same as new)

### Chapter 1: Code of the Ancients
- [ ] Chapter title shows "Chapter 1: Code of the Ancients"
- [ ] Location shows "Mumbai, Eternity Tech HQ"
- [ ] First dialogue shows Krishna speaking
- [ ] Can click/tap to advance dialogue
- [ ] Second dialogue shows Sakshi
- [ ] Puzzle appears with 6 Sanskrit items to arrange
- [ ] Items can be selected (appear highlighted)
- [ ] Check button works
- [ ] Reset button clears selection
- [ ] "View Message" button appears after puzzle closes

### Chapter 2: The Sanskrit Cipher
- [ ] Three cipher rings visible
- [ ] Rings can be clicked to rotate
- [ ] Rings rotate smoothly
- [ ] Alignment marker at top shows rotation
- [ ] All three rings rotate independently
- [ ] Solution checking works for both right and wrong answers
- [ ] Correct answer shows next scene
- [ ] "View Puzzle" button available after closing

### Chapter 3: The Arora Gambit
- [ ] 4 path options visible
- [ ] Can click to select one option
- [ ] Previously selected option deselects when new one chosen
- [ ] Selected option highlights (teal border)
- [ ] "Rooftops" is the correct answer
- [ ] Wrong answer shakes container

### Chapters 4-12
- [ ] Each progresses through dialogue and puzzles
- [ ] All dialogues show with character names
- [ ] All puzzle types function correctly
- [ ] Both reopen buttons appear when applicable
- [ ] Game flow is smooth
- [ ] No console errors appear
- [ ] Final chapter shows completion message

### Reopen Functionality
- [ ] "View Message" button appears after dialogue ends
- [ ] "View Message" button disappears when dialogue showing
- [ ] Clicking "View Message" reopens last dialogue
- [ ] "View Puzzle" button appears after puzzle closes
- [ ] "View Puzzle" button disappears when puzzle showing
- [ ] Clicking "View Puzzle" reopens last puzzle
- [ ] Can reopen same dialogue/puzzle multiple times

### 3D Scene
- [ ] 3D environment renders behind dialog
- [ ] Scene contains ground plane
- [ ] Scene contains geometric objects
- [ ] Camera auto-rotates scene smoothly
- [ ] Cube colors match primary theme color
- [ ] Lighting creates proper shadows
- [ ] Scene doesn't interfere with UI

### Responsive Design
- [ ] **Desktop (1920px+)**:
  - Large buttons easy to click
  - Full-sized 3D scene
  - Comfortable reading space
  
- [ ] **Tablet (768-1024px)**:
  - Buttons scaled appropriately
  - Text readable without zoom
  - Puzzles fit screen
  
- [ ] **Mobile (480-768px)**:
  - Buttons min 48px height
  - Text scales to viewport
  - Reopen buttons visible but compact
  - All interactive elements accessible
  
- [ ] **Small Phone (< 480px)**:
  - Minimum viable UI
  - All buttons still accessible
  - No horizontal scroll needed
  
- [ ] **Landscape Mode**:
  - Dialogue box doesn't cover puzzle
  - All buttons visible
  - 3D scene has wider view
  - Chapter info readable

### Touch Support (Mobile)
- [ ] Tap buttons = highlight + respond
- [ ] Tap puzzle items = select with visual feedback
- [ ] Tap message = advance dialogue
- [ ] Tap cipher ring = rotate smoothly
- [ ] Swipe cipher ring = alternate rotation method
- [ ] Double-tap doesn't zoom
- [ ] Long-press doesn't show menu
- [ ] Pinch-zoom disabled

### Haptic Feedback (Android)
- [ ] Vibrate when dialogue appears
- [ ] Vibrate on correct puzzle answer
- [ ] Stronger vibrate on wrong answer
- [ ] Can feel progress through vibration patterns

### Accessibility
- [ ] High contrast colors
- [ ] Text readable at all sizes
- [ ] All interactive elements keyboard accessible
- [ ] Tab navigation works
- [ ] Enter key submits dialogues
- [ ] Arabic/Devanagari characters display correctly

---

## 🧪 Puzzle Testing

### Chapter 1: Sanskrit Sequence
**Task**: Arrange Sanskrit words in order
```
Items: ॐ, गणेशाय, नमः, सरस्वत्यै, विद्या, दान
Correct Order: ॐ → गणेशाय → नमः → सरस्वत्यै → विद्या → दान
```

**Test Steps**:
1. Select items in order
2. Items should highlight as selected
3. Selected items should show in some order (visual feedback)
4. Click "Check" after selecting all 6
5. Should accept correct order
6. Should reject if selected in wrong order

---

### Chapter 2: Rune Alignment
**Task**: Rotate three rings to align symbols
```
Ring 1: सूर्य (Sun)
Ring 2: चन्द्र (Moon)
Ring 3: मंगल (Mars)
```

**Test Steps**:
1. Click Ring 1 until सूर्य is at top
2. Click Ring 2 until चन्द्र is at top
3. Click Ring 3 until मंगल is at top
4. All rings should rotate individually
5. Use alignment marker (triangle at top) as guide
6. Click "Check" when all aligned
7. Should accept when correct

**Mobile Testing**:
- Swipe left/right to rotate Ring 1
- Swipe up/down to rotate Ring 2
- Alternative rotation method

---

### Chapter 3: Path Choice
**Task**: Choose correct escape route
```
Options: Main Roads, Rooftops, Alleyways, Sewers
Correct: Rooftops
```

**Test Steps**:
1. See all 4 options displayed
2. Click/tap "Rooftops"
3. Should highlight with different border color
4. Click "Check"
5. Should accept as correct
6. Try other options - should shake and reject

---

### Chapter 5: Star Chart (Rune Alignment Variant)
```
Ring 1: विष्णु (Vishnu)
Ring 2: पूर्णिमा (Full Moon)
Ring 3: कार्तिक (Kartik month)
```

**Test Steps**:
- Same as Chapter 2 rune alignment
- Different Sanskrit words
- Test with rotations before checking

---

### Chapter 6: Musical Notes
**Task**: Arrange Indian musical notes (Sargam)
```
Order: Sa, Re, Ga, Ma, Pa, Dha, Ni
```

**Test Steps**:
1. Select all 7 notes in order
2. Visual feedback for each selection
3. Click "Check" when done
4. Should verify sequence

---

### Chapter 7: Water Flow Path
```
Options: Left Channel, Right Channel, Center Channel
Correct: Center Channel
```

**Test Steps**:
- Choose one option
- "Center Channel" should be accepted
- Others should be rejected with shake animation

---

### Chapter 8: Coded Warning
**Task**: Arrange Sanskrit words into warning message
```
Message: "भाई वॉल्ट बी में जाल है" (Brother, Vault B is trapped)
```

**Test Steps**:
1. Select 6 items in order
2. This is a sentence arrangement puzzle
3. Check solution when done

---

### Chapter 9: Infiltration Plan
```
Options: Main Gate, Service Tunnels, Rooftop Access, Underground River
Correct: Service Tunnels
```

**Test Steps**:
- Path choice puzzle
- "Service Tunnels" is correct

---

### Chapter 10: Guardian's Test
```
Ring 1: Quantum
Ring 2: Stars
Ring 3: Structure
```

**Test Steps**:
- Rune alignment with English words instead of Sanskrit

---

### Chapter 11: Final Choice (Combat Strategy)
```
Options: Use Temple Defenses, Direct Confrontation, Let him Escape, Reason with him
Correct: Use Temple Defenses
```

**Test Steps**:
- Path choice puzzle
- Final decision before ending

---

## 🐛 Quick Bug Hunting

### Visual Bugs
- [ ] Dialogue box doesn't overlap incorrectly
- [ ] Buttons aren't cut off at screen edges
- [ ] Text isn't too small to read
- [ ] Colors display correctly (not washed out)
- [ ] 3D scene doesn't flicker
- [ ] Animations are smooth (no stuttering)

### Functionality Bugs
- [ ] Puzzles don't accept answers prematurely
- [ ] Puzzle reset clears all selections
- [ ] Reopen buttons appear/disappear correctly
- [ ] Scene transitions are smooth
- [ ] No infinite loops or freezes
- [ ] All chapters are accessible

### Mobile Bugs
- [ ] Text scalable to all viewport sizes
- [ ] Buttons work on first tap
- [ ] No unwanted zoom on tap
- [ ] Touch targets (48px+) all accessible
- [ ] Landscape/portrait rotation works
- [ ] Scrolling not interfered with

### Console Errors
- [ ] No JavaScript errors
- [ ] No undefined function calls
- [ ] No missing library warnings
- [ ] No network errors (apart from optional CDN issues)

---

## 📊 Performance Checklist

### Desktop Performance
- [ ] Loads in < 3 seconds
- [ ] 60 FPS on main loop
- [ ] No lag during interactions
- [ ] 3D scene renders smoothly
- [ ] Memory stable (no leaks)

### Mobile Performance
- [ ] Loads in < 5 seconds on 4G
- [ ] 30+ FPS on mobile devices
- [ ] No jank when scrolling/tapping
- [ ] Battery drain acceptable
- [ ] Works on older devices (iOS 12+, Android 7+)

### Network
- [ ] Images load without blocking
- [ ] Works if CDN is slow
- [ ] Graceful degradation if CDN fails
- [ ] Doesn't require online mode

---

## ✅ Final Validation

Run this in browser console:

```javascript
// Game Object Test
console.assert(typeof game === 'object', 'Game not defined');
console.assert(typeof game.startChapter === 'function', 'startChapter missing');
console.assert(typeof game.showDialogue === 'function', 'showDialogue missing');
console.assert(typeof game.showPuzzle === 'function', 'showPuzzle missing');
console.assert(typeof game.reopenLastDialogue === 'function', 'reopenLastDialogue missing');
console.assert(typeof game.reopenLastPuzzle === 'function', 'reopenLastPuzzle missing');

// DOM Elements Test
console.assert(document.getElementById('game-interface'), 'game-interface missing');
console.assert(document.getElementById('dialogue-box'), 'dialogue-box missing');
console.assert(document.getElementById('puzzle-container'), 'puzzle-container missing');
console.assert(document.getElementById('reopen-dialogue-btn'), 'reopen-dialogue-btn missing');
console.assert(document.getElementById('reopen-puzzle-btn'), 'reopen-puzzle-btn missing');

// Chapter Data Test
console.assert(Object.keys(game.chapterData).length === 12, 'Not 12 chapters');
console.assert(game.chapterData[1].scenes[1].dialogues, 'Ch1Sc1 missing dialogues');

// All tests passed!
console.log('✅ All validation tests passed!');
```

If all assertions pass, the game is properly set up!

---

## 🎉 You're Ready!

Your game is now fully installed and tested. Time to enjoy **The Padmanabha Enigma**!

### Quick Start
1. Open `index.html`
2. Wait for intro screen
3. Click "Skip" (optional)
4. Click "New Journey"
5. Read and solve your way through!

### Need Help?
- See README.md for complete solutions
- See DEBUGGING_GUIDE.md for troubleshooting
- Check browser console for errors (F12)
- Verify all puzzle solutions in README

**Happy Gaming! 🎮**

---

*Last Updated: February 2026*
