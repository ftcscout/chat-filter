# Chat Filter - Advanced Profanity Detection System

## Core Components

### 1. Word Detection System

- **Trie-based Word Lookup**: Implements a trie data structure for efficient profanity word matching
- **Blacklist Set**: Contains base profanity words and their variations
- **Problematic Substrings Map**: Handles legitimate words that contain profanity substrings (e.g., "assassin" contains "ass")

### 2. Pattern Recognition

- **Leetspeak Detection**: Identifies character substitutions (e.g., "f*ck", "sh1t", "a$$")
- **Character Insertion Patterns**: Detects profanity with inserted characters (e.g., "f.u.c.k", "s-h-i-t")
- **Verb Form Detection**: Recognizes conjugated forms (e.g., "fucking", "fucked", "fucks")
- **Repeated Character Handling**: Processes words with repeated letters (e.g., "fuuuuck")

### 3. Context Analysis

- **Word Boundary Checking**: Ensures profanity is detected as standalone words
- **Dictionary Validation**: Uses English dictionary to prevent false positives
- **Context-Aware Processing**: Considers surrounding text for better accuracy

## Implementation Details

### Initialization

```javascript
const profanityFilter = require('./profanities.js');
profanityFilter.init({
    strictness: 'medium',     // Does not change any filtration (at least not yet)
    checkWordBoundaries: true, // Check for word boundaries
    allowRepeatedLetters: false, // If we should allow repeated chars or not (Ex. assssssss)
    checkLeetSpeak: true,     // Detect leetspeak variations
    useRegexForQuickCheck: true, // Use regex for initial screening (Nice optimization for speed if you need it)
    useDictionary: true       // Use dictionary for validation (Significantly improves performance)
});
```

### Core Detection Methods

1. **Basic Word Matching**
   - Direct comparison against blacklist
   - Case-insensitive matching
   - Word boundary validation

2. **Pattern Recognition**
   - Leetspeak pattern matching using regex
   - Character insertion detection
   - Verb form identification

3. **Context Processing**
   - Dictionary validation
   - Word boundary analysis
   - Substring context checking

### Testing System

Run the test suite:

```bash
node profanity-tester.js
```

The test suite includes:

1. **Single Message Testing**
   - Test individual messages
   - Get detailed detection results
   - Performance metrics

2. **Preset Test Cases**
   - Basic profanity detection
   - Leetspeak variations
   - Word boundary cases
   - False positive prevention

3. **Edge Case Generator**
   - Generates various profanity variations
   - Tests detection accuracy
   - Performance benchmarking

## Performance Optimization

1. **Trie Implementation**
   - O(n) lookup time for words
   - Efficient memory usage
   - Fast pattern matching

2. **Regex Optimization**
   - Quick initial screening
   - Pattern-based detection
   - Efficient character substitution handling

3. **Dictionary Caching**
   - On-demand loading
   - Memory-efficient storage
   - Fast word validation

## Usage Examples

### Basic Usage

```javascript
const isClean = profanityFilter.isClean("Your message here");
if (!isClean) {
    console.log("Profanity detected!");
}
```

### Advanced Usage

```javascript
// Check with custom settings
profanityFilter.init({
    strictness: 'high',
    checkWordBoundaries: true
});

// Process multiple messages
const messages = ["Message 1", "Message 2"];
messages.forEach(msg => {
    if (!profanityFilter.isClean(msg)) {
        console.log(`Profanity in: ${msg}`);
    }
});
```

## Contributing

To contribute:

1. Fork the repository
2. Create a feature branch
3. Submit a pull request
