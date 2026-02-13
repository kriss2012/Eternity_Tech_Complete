# 🔧 Eternity Tech - Debugging & Testing Guide

## Quick Debugging Checklist

### Pre-Game Launch
- [ ] Browser console shows no errors
- [ ] JavaScript enabled
- [ ] Cookies/LocalStorage enabled
- [ ] WebGL supported (check: `webglsupport.info`)
- [ ] All CDN libraries loaded (Three.js, Fonts)

### Game Launch Tests
```javascript
// Run these in browser console (F12)

// 1. Check Three.js
console.assert(typeof THREE !== 'undefined', 'Three.js not loaded');

// 2. Check game initialization
console.assert(typeof game !== 'undefined', 'Game not initialized');

// 3. Check initial state
console.assert(game.gameState === 'backstory', 'Wrong initial state');

// 4. Check DOM elements
console.assert(document.getElementById('game-interface'), 'Game interface missing');
console.assert(document.getElementById('dialogue-box'), 'Dialogue box missing');
console.assert(document.getElementById('puzzle-container'), 'Puzzle container missing');
```

---

## State Verification Tests

### Check Game State Transitions
```javascript
// Log all state changes
const originalSetState = game.setState.bind(game);
game.setState = function(newState) {
    console.log(`STATE: ${this.gameState} → ${newState}`);
    originalSetState(newState);
};

// Or manually check states
console.log('Valid states:', ['loading', 'backstory', 'menu', 'dialogue', 'puzzle', 'playing']);
console.log('Current state:', game.gameState);
```

### Verify Chapter Data
```javascript
// Check all chapters exist
Object.keys(game.chapterData).forEach(ch => {
    const chapter = game.chapterData[ch];
    console.log(`Chapter ${ch}: "${chapter.title}" at ${chapter.location}`);
});

// Check specific chapter
const ch = game.chapterData[1];
console.log('Chapter 1 scenes:', Object.keys(ch.scenes).length);
```

---

## Dialogue System Testing

### Test Basic Dialogue
```javascript
// Show test dialogue
game.showDialogue({
    c: "Test Character",
    t: "This is a test message",
    emotion: "excited"
});

// Check dialogue was stored
console.log('Last Dialogue:', game.lastDialogue);

// Check reopen button visible
console.log('Reopen button hidden?', 
    document.getElementById('reopen-dialogue-btn').classList.contains('hide-reopen')
);
```

### Test Dialogue Flow
```javascript
// Advance to Chapter 1, Scene 1
game.startChapter(1);

// Process dialogues
game.currentDialogueIndex = -1;
game.nextDialogue(); // Show first dialogue
game.nextDialogue(); // Show second dialogue
game.nextDialogue(); // Progress scene
```

### Test Reopen Functionality
```javascript
// Navigate to next state
game.handleSceneEnd();

// Try reopening dialogue
game.reopenLastDialogue();

// Should show dialogue again
console.assert(game.gameState === 'dialogue', 'Dialogue not reopened');
```

---

## Puzzle System Testing

### Test Puzzle Generation
```javascript
// Create test puzzle
const testPuzzle = {
    type: "path_choice",
    title: "Test Puzzle",
    desc: "Choose the correct answer",
    items: ["Option A", "Option B", "Option C"],
    solution: "Option B"
};

// Generate puzzle
game.puzzleSystem.generatePuzzle(testPuzzle);

// Check if puzzle appeared
console.assert(
    document.getElementById('puzzle-container').classList.contains('active'),
    'Puzzle not showing'
);
```

### Test Puzzle Types
```javascript
// Test Sanskrit Sequence Puzzle
const sanskritPuzzle = {
    type: "sanskrit_sequence",
    title: "Sanskrit Test",
    desc: "Arrange in order",
    items: ["नमः", "सत्यम्", "शिवम्"],
    solution: ["सत्यम्", "शिवम्", "नमः"]
};
game.puzzleSystem.generatePuzzle(sanskritPuzzle);

// Test Rune Alignment Puzzle
const runePuzzle = {
    type: "rune_alignment",
    title: "Rune Test",
    desc: "Align the rings",
    rings: [['A', 'B'], ['X', 'Y'], ['1', '2']],
    solution: ['A', 'X', '1']
};
game.puzzleSystem.generatePuzzle(runePuzzle);

// Test Path Choice Puzzle
const pathPuzzle = {
    type: "path_choice",
    title: "Path Test",
    desc: "Choose wisely",
    items: ["Path 1", "Path 2", "Path 3"],
    solution: "Path 2"
};
game.puzzleSystem.generatePuzzle(pathPuzzle);
```

### Test Solution Checking
```javascript
// For Path Choice
game.puzzleSystem.selectedItems = ["Rooftops"];
game.puzzleSystem.currentPuzzle = {
    type: "path_choice",
    solution: "Rooftops"
};
game.puzzleSystem.checkSolution(); // Should pass

// For Sanskrit Sequence
game.puzzleSystem.selectedItems = ["ॐ", "गणेशाय", "नमः"];
game.puzzleSystem.currentPuzzle = {
    type: "sanskrit_sequence",
    solution: ["ॐ", "गणेशाय", "नमः"]
};
game.puzzleSystem.checkSolution(); // Should pass

// For Rune Alignment
game.puzzleSystem.ringRotations = [0, 0, 0];
game.puzzleSystem.currentPuzzle = {
    type: "rune_alignment",
    rings: [['सूर्य', 'चन्द्र'], ['चन्द्र'], ['मंगल']],
    solution: ['सूर्य', 'चन्द्र', 'मंगल']
};
game.puzzleSystem.checkSolution(); // Adjust rotations as needed
```

---

## Mobile/Touch Testing

### Verify Touch Support
```javascript
// Check if mobile device detected
console.log('Is Mobile:', game.isMobileDevice());

// Check touch event support
console.log('Touch Events:', () => 'ontouchstart' in window);

// Check vibration API
console.log('Vibration API:', () => 'vibrate' in navigator);

// Test vibration
navigator.vibrate([100, 50, 100]);
```

### Test Responsive Breakpoints
```javascript
// Check viewport
console.log('Viewport Width:', window.innerWidth);
console.log('Viewport Height:', window.innerHeight);

// Check touch target sizes
const buttons = document.querySelectorAll('.menu-button');
buttons.forEach((btn, i) => {
    const rect = btn.getBoundingClientRect();
    console.log(`Button ${i}: ${rect.width}x${rect.height}px`);
    console.assert(rect.height >= 48, `Button ${i} too small for touch`);
});
```

### Test Orientation Change
```javascript
// Simulate orientation change
window.dispatchEvent(new Event('orientationchange'));

// Check if layout updated
setTimeout(() => {
    console.log('New Viewport:', window.innerWidth, 'x', window.innerHeight);
}, 100);
```

---

## 3D Scene Testing

### Test Three.js Rendering
```javascript
// Check if scene exists
console.assert(game.scene instanceof THREE.Scene, 'Scene not created');
console.assert(game.camera instanceof THREE.Camera, 'Camera not created');
console.assert(game.renderer instanceof THREE.WebGLRenderer, 'Renderer not created');

// Check scene contents
console.log('Objects in scene:', game.scene.children.length);
console.log('Scene objects:', game.scene.children.map(obj => obj.type));
```

### Test Camera
```javascript
// Check camera position
console.log('Camera Position:', game.camera.position);
console.log('Camera Target:', game.controls.target);

// Test controls
console.log('Controls enabled:', !game.controls.autoRotate ? 'No' : 'Yes (auto)');
console.log('Damping:', game.controls.enableDamping ? 'Enabled' : 'Disabled');
```

### Test Lighting
```javascript
// Check lights
const lights = game.scene.children.filter(obj => obj instanceof THREE.Light);
console.log('Number of lights:', lights.length);
lights.forEach((light, i) => {
    console.log(`Light ${i}:`, light.type, 'Intensity:', light.intensity);
});
```

---

## Event Listener Testing

### Test Button Events
```javascript
// Test reopen dialogue button
const reopenDialogueBtn = document.getElementById('reopen-dialogue-btn');
reopenDialogueBtn.dispatchEvent(new Event('click'));
console.log('Reopen dialogue triggered');

// Test reopen puzzle button
const reopenPuzzleBtn = document.getElementById('reopen-puzzle-btn');
reopenPuzzleBtn.dispatchEvent(new Event('click'));
console.log('Reopen puzzle triggered');
```

### Test Keyboard Events
```javascript
// Simulate SPACE key
const spaceEvent = new KeyboardEvent('keydown', {
    code: 'Space',
    key: ' '
});
window.dispatchEvent(spaceEvent);
console.log('SPACE key simulated');

// Simulate ESC key
const escEvent = new KeyboardEvent('keydown', {
    code: 'Escape',
    key: 'Escape'
});
window.dispatchEvent(escEvent);
console.log('ESC key simulated');
```

### Test Touch Events
```javascript
// Simulate touch on dialogue
const touchEvent = new TouchEvent('touchend', {
    bubbles: true,
    cancelable: true,
    touches: []
});
document.getElementById('dialogue-box').dispatchEvent(touchEvent);
console.log('Touch simulated on dialogue');
```

---

## Storage & Progress Testing

### Check Browser Storage
```javascript
// Check LocalStorage
console.log('LocalStorage available:', typeof(Storage) !== 'undefined');
console.log('LocalStorage items:', Object.keys(localStorage).length);

// Check if progress saved
console.log('Saved Chapter:', localStorage.getItem('eternity_chapter'));
console.log('Saved Scene:', localStorage.getItem('eternity_scene'));

// Manual save
localStorage.setItem('eternity_chapter', game.currentChapter);
localStorage.setItem('eternity_scene', game.currentScene);
```

---

## Performance Testing

### Monitor FPS and Performance
```javascript
// Monitor frame rate
let frameCount = 0;
let lastTime = Date.now();

const originalAnimate = game.animate.bind(game);
game.animate = function() {
    frameCount++;
    const currentTime = Date.now();
    if (currentTime - lastTime >= 1000) {
        console.log(`FPS: ${frameCount}`);
        frameCount = 0;
        lastTime = currentTime;
    }
    originalAnimate();
};
```

### Check Memory Usage
```javascript
// Chrome DevTools: Performance > Memory
const memory = performance.memory;
console.log('Used JS Heap:', (memory.usedJSHeapSize / 1048576).toFixed(2), 'MB');
console.log('Total JS Heap:', (memory.totalJSHeapSize / 1048576).toFixed(2), 'MB');
console.log('JS Heap Limit:', (memory.jsHeapSizeLimit / 1048576).toFixed(2), 'MB');
```

---

## Common Bug Fixes

### Bug: Dialogue Doesn't Show
**Cause**: `gameState` not set to 'dialogue'
```javascript
// Fix:
game.setState('dialogue');
game.showDialogue(dialogueData);
```

### Bug: Puzzle Solution Always Wrong
**Cause**: String comparison with extra spaces
```javascript
// Fix:
const selectedText = item.textContent.trim();
// instead of
const selectedText = item.textContent;
```

### Bug: Reopen Buttons Don't Appear
**Cause**: Not calling `updateReopenButtons()`
```javascript
// Fix: Add at end of methods that change state
game.updateReopenButtons();
```

### Bug: Touch Events Not Firing
**Cause**: `preventDefault()` not called or event delegation issue
```javascript
// Fix:
element.addEventListener('touchend', (e) => {
    e.preventDefault(); // Required
    // Handle action
});
```

### Bug: 3D Scene Doesn't Render on Mobile
**Cause**: WebGL not supported or pixel ratio too high
```javascript
// Fix in initThreeJS:
if (isMobile) {
    this.renderer.setPixelRatio(Math.min(window.devicePixelRatio, 2));
}
```

### Bug: Cipher Wheel Won't Rotate
**Cause**: Touch event not reaching ring element
```javascript
// Fix: Ensure ring element has proper event listeners
ringEl.addEventListener('click', () => this.rotateRing(i));
ringEl.addEventListener('touchend', (e) => {
    e.preventDefault();
    this.rotateRing(i);
});
```

---

## Console Command Reference

```javascript
// Navigation
game.startChapter(1);           // Go to chapter 1
game.startScene(1, 1);          // Go to chapter 1, scene 1
game.startNewGame();            // New game
game.showMainMenu();            // Back to menu

// Dialogue
game.showDialogue({c:"Test", t:"Message"}); // Show dialogue
game.reopenLastDialogue();      // Reopen dialogue
game.nextDialogue();            // Next dialogue

// Puzzles
game.showPuzzle(puzzleData);    // Show puzzle
game.reopenLastPuzzle();        // Reopen puzzle
game.closePuzzle();             // Close puzzle
game.puzzleSystem.resetPuzzle(); // Reset puzzle
game.puzzleSystem.checkSolution(); // Check answer

// State Management
game.setState(newState);        // Change state
game.updateReopenButtons();     // Update UI buttons

// Debugging
console.log(game.gameState);    // Current state
console.log(game.lastDialogue); // Last dialogue
console.log(game.lastPuzzleData); // Last puzzle
console.log(game.currentChapter, game.currentScene); // Position

// Mobile
console.log(game.isMobileDevice()); // Check if mobile
navigator.vibrate([100, 50, 100]); // Test vibration
```

---

## Testing Checklist

### Full Game Playthrough
- [ ] **Chapter 1**: Code of the Ancients
  - [ ] Dialogue shows correctly
  - [ ] Sanskrit Sequence puzzle works
  - [ ] Can select items in order
  - [ ] Correct answer accepted
  - [ ] Scene advances properly
  
- [ ] **Chapter 2**: The Sanskrit Cipher
  - [ ] Rune Alignment puzzle appears
  - [ ] Can rotate cipher rings
  - [ ] Ring rotation works correctly
  - [ ] Solution checking works
  
- [ ] **Chapter 3**: The Arora Gambit
  - [ ] Path Choice puzzle shows all options
  - [ ] Can select one option
  - [ ] Correct path chosen
  
- [ ] **Chapters 4-12**: All scenarios
  - [ ] Dialogue displays properly
  - [ ] Puzzles appear correctly
  - [ ] Solutions are accepted
  - [ ] Chapter progression works

### Feature Testing
- [ ] Reopen Dialogue button shows when needed
- [ ] Reopen Puzzle button shows when needed
- [ ] Buttons hide when not applicable
- [ ] 3D scene renders in background
- [ ] Scene rotates smoothly
- [ ] Responsive layout on different sizes
- [ ] Touch controls work on mobile
- [ ] Haptic feedback triggers on Android
- [ ] Safari works on iOS
- [ ] Chrome works on Android

### Edge Cases
- [ ] Rapid button clicks handled
- [ ] Switching between dialogue/puzzle works
- [ ] Window resize doesn't break layout
- [ ] Orientation change works
- [ ] Zooming doesn't break UI
- [ ] Mobile back button behavior
- [ ] Offline functionality (CDN fails)

---

## Performance Optimization Tips

### For Desktop
- Enable hardware acceleration
- Use Chrome/Firefox for best performance
- Close unnecessary tabs
- Check for background processes

### For Mobile
- Close other apps
- Enable GPU acceleration in browser settings
- Use WiFi for better CDN loading
- Clear browser cache periodically

---

**Last Updated: February 2026**
*Keep this guide handy for troubleshooting!*
