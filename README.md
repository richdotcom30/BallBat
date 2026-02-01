# 🤖 BallBat Bot - The Football Prediction Robot ⚽💰

[![Python](https://img.shields.io/badge/Python-3.9+-blue.svg)](https://python.org)
[![License](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)
[![Status](https://img.shields.io/badge/Status-Production%20Ready-orange.svg)](docs/INSTALL.md)

**A smart robot that watches football games and guesses if BOTH teams will score!** 🎯

> **"Like having a football expert in your computer!"** ⭐

## 📋 Table of Contents

- [🚀 Quick Start](#-quick-start)
- [🔧 Installation](#-installation)
- [🎮 Usage](#-usage)
- [⚙️ Configuration](#️-configuration)
- [📊 Output Formats](#-output-formats)
- [🏗️ Project Structure](#-project-structure)
- [🧪 Testing](#-testing)
- [🐛 Troubleshooting](#-troubleshooting)
- [📚 Documentation](#-documentation)
- [⚠️ Important Notes](#️-important-notes)

## 🚀 Quick Start

### 1. Prerequisites
- Python 3.9 or higher
- Chrome browser (for web scraping)
- Git (for cloning the repository)

### 2. Installation
```bash
# Clone the repository
git clone https://github.com/richdotcom30/BallBat.git
cd BallBat

# Install dependencies
pip install -r requirements.txt

# Run the setup script (automatically installs ChromeDriver)
python scripts/setup.py
```

### 3. Basic Usage
```bash
# Run with default settings
python main.py

# Run for specific leagues
python main.py --leagues "England-Premier-League,Spain-La-Liga"

# Run for tomorrow's matches
python main.py --days-ahead 1

# Run in headless mode (no browser window)
python main.py --headless true
```

### 4. View Results
Results are saved to:
- `outputs/predictions.csv` - CSV format
- `outputs/predictions.json` - JSON format
- Console output - Real-time predictions

## 🔧 Installation

### System Requirements
- **Operating System**: Windows 10+, macOS 10.14+, Linux
- **Python**: 3.9 or higher
- **Memory**: 4GB RAM minimum, 8GB recommended
- **Storage**: 100MB free space

### Step-by-Step Installation

1. **Install Python**
   - Download from [python.org](https://python.org)
   - Make sure to check "Add Python to PATH" during installation

2. **Clone Repository**
   ```bash
   git clone https://github.com/richdotcom30/BallBat.git
   cd BallBat
   ```

3. **Install Dependencies**
   ```bash
   # Install required packages
   pip install -r requirements.txt
   
   # Install development dependencies (optional)
   pip install -r requirements-dev.txt
   ```

4. **Setup Environment**
   ```bash
   # Run the automated setup script
   python scripts/setup.py
   
   # This will:
   # - Install ChromeDriver automatically
   # - Create necessary directories
   # - Set up configuration files
   ```

5. **Configure Settings**
   - Copy `.env.example` to `.env`
   - Edit `.env` with your preferences (see Configuration section)

6. **Test Installation**
   ```bash
   # Run a quick test
   python main.py --test
   
   # Should output: "✅ All systems operational!"
   ```

## 🎮 Usage

### Basic Commands

```bash
# Default prediction run
python main.py

# Specify leagues to analyze
python main.py --leagues "England-Premier-League,Spain-La-Liga,Germany-Bundesliga"

# Predict for specific number of days ahead
python main.py --days-ahead 3

# Set minimum confidence threshold (0-100%)
python main.py --min-confidence 70

# Output format options
python main.py --output csv    # CSV format
python main.py --output json   # JSON format
python main.py --output both   # Both formats

# Browser options
python main.py --headless true    # No browser window
python main.py --headless false   # Show browser window

# Debug mode
python main.py --debug true       # Verbose logging
```

### Advanced Usage

```bash
# Complete example with all options
python main.py \
  --leagues "England-Premier-League,Spain-La-Liga" \
  --days-ahead 2 \
  --min-confidence 65 \
  --output both \
  --headless true \
  --debug false

# Run specific strategies only
python main.py --strategy btts-only
python main.py --strategy value-bets

# Custom configuration file
python main.py --config custom_config.json
```

### Command Line Options

| Option | Description | Default | Example |
|--------|-------------|---------|---------|
| `--leagues` | Comma-separated league list | All available | `"Premier-League,La-Liga"` |
| `--days-ahead` | Days to predict ahead | 1 | `3` |
| `--min-confidence` | Minimum confidence % | 50 | `70` |
| `--output` | Output format | csv | `json` |
| `--headless` | Run browser hidden | false | `true` |
| `--debug` | Enable debug logging | false | `true` |
| `--test` | Test mode | false | `true` |
| `--config` | Custom config file | .env | `custom.json` |

## ⚙️ Configuration

### Environment Variables (`.env`)

Create a `.env` file in the project root:

```env
# Web Scraping Settings
HEADLESS_MODE=true
WEBDRIVER_TIMEOUT=30
MAX_RETRIES=3
REQUEST_DELAY=2

# Prediction Settings
MIN_CONFIDENCE=50
MIN_ODDS=1.5
MAX_ODDS=5.0
BTTS_THRESHOLD=0.6

# Output Settings
OUTPUT_FORMAT=csv
OUTPUT_DIR=outputs
LOG_LEVEL=INFO

# League Configuration
ENABLED_LEAGUES=England-Premier-League,Spain-La-Liga,Germany-Bundesliga,Italy-Serie-A,France-Ligue-1

# Advanced Settings
POISSON_LAMBDA_HOME=1.5
POISSON_LAMBDA_AWAY=1.2
KELLY_FRACTION=0.25
```

### League Configuration

Available leagues (use exact names):
- `England-Premier-League`
- `Spain-La-Liga`
- `Germany-Bundesliga`
- `Italy-Serie-A`
- `France-Ligue-1`
- `Netherlands-Eredivisie`
- `Portugal-Primeira-Liga`
- `Belgium-First-Division-A`
- `Turkey-Super-Lig`
- `Scotland-Premiership`

### Custom Configuration

For advanced users, create a JSON configuration file:

```json
{
  "scraping": {
    "headless": true,
    "timeout": 30,
    "retries": 3
  },
  "prediction": {
    "min_confidence": 60,
    "btts_threshold": 0.65,
    "kelly_fraction": 0.25
  },
  "output": {
    "format": "both",
    "directory": "custom_outputs"
  }
}
```

## 📊 Output Formats

### CSV Output (`outputs/predictions.csv`)
```csv
match_id,home_team,away_team,league,date,btts_probability,confidence,recommendation,odds,expected_value
1,Arsenal,Tottenham,Premier League,2026-01-30,0.78,78.0,True,1.90,12.5
2,Chelsea,Man City,Premier League,2026-01-31,0.35,35.0,False,2.10,-5.2
```

### JSON Output (`outputs/predictions.json`)
```json
[
  {
    "match_id": 1,
    "home_team": "Arsenal",
    "away_team": "Tottenham",
    "league": "Premier League",
    "date": "2026-01-30",
    "btts_probability": 0.78,
    "confidence": 78.0,
    "recommendation": true,
    "odds": 1.90,
    "expected_value": 12.5,
    "analysis": {
      "home_goals_avg": 1.8,
      "away_goals_avg": 1.6,
      "btts_history": 0.7,
      "league_btts_rate": 0.62
    }
  }
]
```

### Console Output
```
🤖 BALLBAT BOT IS WORKING... ⚽

🎯 PREDICTION RESULTS:
========================

Match: Arsenal vs Tottenham
League: Premier League
Date: 2026-01-30

Both Teams Score? YES! 🎯
Confidence: 78%
Expected Value: +12.5%

Reasons:
✅ Both teams scored in 7/10 recent games
✅ Average goals: 2.1 per game
✅ Head-to-head: Both scored in 4/5 meetings
✅ League BTTS rate: 62% (High!)

Recommendation: BET ON BTTS @ Odds 1.90
Optimal Stake: £25.00 (1/4 Kelly)
Risk Level: Medium

========================
Next update: Tomorrow 8:00 AM
```

## 🏗️ Project Structure

```
BallBat/
├── main.py              # Main entry point
├── scripts/             # Utility scripts
│   ├── setup.py         # Automated setup
│   └── README.md        # Script documentation
├── src/                 # Source code
│   ├── __init__.py
│   ├── bot.py           # Main bot logic
│   ├── config/          # Configuration management
│   ├── predictor/       # Prediction algorithms
│   │   ├── __init__.py
│   │   ├── btts_strategy.py    # BTTS strategy
│   │   ├── poisson_model.py    # Poisson model
│   │   └── value_detector.py   # Value detection
│   ├── scraper/         # Web scraping
│   │   ├── __init__.py
│   │   ├── base_scraper.py     # Base scraper class
│   │   ├── flashscore_scraper.py # Flashscore implementation
│   │   ├── sofascore_scraper.py  # SofaScore implementation
│   │   └── multi_source_scraper.py # Multi-source coordination
│   └── utils/           # Utility functions
│       ├── __init__.py
│       ├── output_manager.py   # Output handling
│       └── test_utils.py       # Testing utilities
├── data/                # Data storage
│   ├── cache/           # Cached data
│   └── raw/             # Raw scraped data
├── outputs/             # Prediction outputs
├── tests/               # Test files
│   ├── unit/            # Unit tests
│   ├── integration/     # Integration tests
│   └── fixtures/        # Test data
├── docs/                # Documentation
│   └── BOT_OPERATION.md # Operation guide
├── logs/                # Application logs
├── requirements.txt     # Production dependencies
├── requirements-dev.txt # Development dependencies
├── .env.example         # Environment template
├── .gitignore           # Git ignore rules
└── README.md            # This file
```

## 🧪 Testing

### Run All Tests
```bash
# Run all tests
python -m pytest tests/

# Run with coverage
python -m pytest tests/ --cov=src

# Run specific test file
python -m pytest tests/unit/test_btts_strategy.py

# Run integration tests
python -m pytest tests/integration/
```

### Test Modes
```bash
# Quick test mode
python main.py --test

# Full system test
python main.py --test --full

# Unit tests only
python -m pytest tests/unit/

# Integration tests only
python -m pytest tests/integration/
```

### Test Coverage
```bash
# Install coverage tool
pip install coverage

# Run tests with coverage
coverage run -m pytest tests/
coverage report
coverage html  # Generate HTML report
```

## 🐛 Troubleshooting

### Common Issues

**1. ChromeDriver Not Found**
```bash
# Solution: Run setup script
python scripts/setup.py
```

**2. Import Errors**
```bash
# Solution: Reinstall dependencies
pip install -r requirements.txt --force-reinstall
```

**3. Web Scraping Timeout**
```bash
# Solution: Increase timeout in .env
WEBDRIVER_TIMEOUT=60
```

**4. No Predictions Generated**
```bash
# Solution: Check league configuration
# Ensure leagues are correctly spelled in .env
ENABLED_LEAGUES=England-Premier-League,Spain-La-Liga
```

**5. Permission Errors (Windows)**
```bash
# Solution: Run as administrator
# Or check file permissions
```

### Debug Mode
```bash
# Enable debug logging
python main.py --debug true

# Check logs in outputs/logs/
```

### Manual ChromeDriver Setup
If automatic setup fails:

1. Download ChromeDriver from [chromedriver.chromium.org](https://chromedriver.chromium.org)
2. Extract to `BallBat/data/drivers/`
3. Ensure it matches your Chrome version

### Performance Issues
```bash
# Reduce number of leagues
--leagues "England-Premier-League"

# Reduce prediction days
--days-ahead 1

# Enable headless mode
--headless true
```

## 📚 Documentation

### Available Documentation
- **[Installation Guide](docs/INSTALL.md)** - Detailed installation instructions
- **[Bot Operation Guide](docs/BOT_OPERATION.md)** - How the bot works
- **[Strategy Documentation](docs/STRATEGY.md)** - Prediction strategies
- **[Technical Documentation](docs/TECHNICAL.md)** - Technical implementation details

### Code Documentation
All code is documented with docstrings. Use:
```python
help(module_name)
help(class_name)
help(function_name)
```

## ⚠️ Important Notes

### 🎲 Gambling Warning
> **This robot is for educational and research purposes only! Gambling can be addictive and dangerous. Never bet money you cannot afford to lose. Always gamble responsibly and seek help if needed.**

### 📚 Educational Purpose
- **Learning tool** for understanding football statistics and betting
- **Research project** for sports analytics
- **Programming example** for web scraping and data analysis
- **Math education** for probability and statistics

### 🌐 Legal Compliance
- Follows all web scraping best practices
- Respects website terms of service
- For personal, non-commercial use only
- Users are responsible for local gambling laws

### 🔒 Data Privacy
- No personal data collection
- Local data storage only
- No cloud dependencies
- User-configurable data retention

### 🚀 Future Development
- Multi-sport support (basketball, tennis)
- Machine learning enhancements
- Mobile app interface
- Real-time betting integration

---

## 🤖 Meet BallBat Bot!

```
    🤖🤖🤖🤖🤖🤖🤖🤖🤖🤖
    🤖                🤖
    🤖   ⚽⚽⚽⚽⚽   🤖
    🤖  ⚽        ⚽  🤖
    🤖 ⚽  FOOTBALL ⚽ 🤖
    🤖  ⚽        ⚽  🤖
    🤖   ⚽⚽⚽⚽⚽   🤖
    🤖                🤖
    🤖🤖🤖🤖🤖🤖🤖🤖🤖🤖
    
    "I'M READY TO ANALYZE FOOTBALL! ⚽"
```

**BallBat Bot** - Your intelligent football prediction assistant! 🤖⚽📊

*Made with ❤️ for football fans, data scientists, and curious minds everywhere!*

---

**⚠️ Remember: This is an educational tool. Always gamble responsibly and within legal boundaries.**