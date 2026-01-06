# SafeBrowse-AI Browser Extension

This directory contains the Chrome/Edge Manifest V3 browser extension for real-time phishing URL detection.

## 📁 Structure

```
extension/
├── manifest.json          # Extension configuration
├── background.js          # Service worker (ML inference)
├── feature_extractor.js   # URL feature extraction (17 features)
├── popup.html            # Extension popup UI
├── popup.js              # Popup logic
├── model_export.json     # LightGBM model (auto-generated)
└── icons/                # Extension icons (to be added)
```

## 🚀 Installation

1. **Export the model first:**
   ```bash
   cd ..
   python export_model.py
   ```

2. **Load extension in Chrome/Edge:**
   - Open `chrome://extensions/`
   - Enable "Developer mode"
   - Click "Load unpacked"
   - Select this `extension/` directory

3. **Test the extension:**
   - Visit any website
   - Click the extension icon to see the risk score
   - Suspicious sites (score > 0.5) trigger automatic warnings

## 🎨 Icons (To Add)

Create three icon sizes in `icons/` folder:
- `icon16.png` - 16×16 pixels
- `icon48.png` - 48×48 pixels  
- `icon128.png` - 128×128 pixels

## 🔧 How It Works

1. **Background Service Worker** monitors all tab updates
2. **Feature Extraction** mirrors Python implementation (17 lexical features)
3. **LightGBM Inference** traverses decision trees in JavaScript
4. **Real-time Alerts** for sites with risk score > 50%
5. **Popup Display** shows detailed analysis for current tab

## 📊 Features Extracted

- URL length, host length, path length, query length
- Character counts (digits, hyphens, @, %, ?, =, /, dots)
- IP address detection
- Shannon entropy
- TLD/subdomain/domain lengths
- HTTPS usage

## 🔐 Privacy

- All processing happens locally in the browser
- No data sent to external servers
- Model runs entirely client-side

## 🎯 Future Enhancements

- [ ] Add CNN/TensorFlow.js model for char-level analysis
- [ ] Ensemble prediction (LightGBM + CNN)
- [ ] Whitelist/blacklist management
- [ ] Detailed threat analysis view
- [ ] Integration with Google Safe Browsing API
