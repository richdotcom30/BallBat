# Installation Guide

## System Requirements

### Minimum Requirements
- **Operating System**: Windows 10/11, macOS 10.14+, or Linux
- **Python**: 3.9 or higher
- **RAM**: 4GB minimum, 8GB recommended
- **Storage**: 500MB free space
- **Internet Connection**: Required for data scraping

### Browser Requirements
- **Google Chrome** (version 90+) or **Chromium** browser
- **ChromeDriver** (automatically managed via webdriver-manager)

## Quick Installation

### 1. Clone the Repository
```bash
git clone https://github.com/yourusername/BallBat.git
cd BallBat
```

### 2. Create Virtual Environment (Recommended)
```bash
# Create virtual environment
python -m venv venv

# Activate virtual environment
# On Windows:
venv\Scripts\activate

# On macOS/Linux:
source venv/bin/activate
```

### 3. Install Dependencies
```bash
pip install -r requirements.txt
```

### 4. Configure Environment
```bash
# Copy example environment file
cp .env.example .env

# Edit .env file with your preferences
notepad .env  # Windows
# or
nano .env     # macOS/Linux
```

### 5. Test Installation
```bash
python main.py --test
```

## Detailed Installation Steps

### Python Environment Setup

#### Windows Installation
1. **Download Python**
   - Visit [python.org](https://python.org)
   - Download Python 3.9+ installer
   - Run installer with "Add Python to PATH" checked

2. **Verify Installation**
   ```bash
   python --version
   pip --version
   ```

3. **Create Virtual Environment**
   ```bash
   python -m venv ballbat-env
   ballbat-env\Scripts\activate
   ```

#### macOS Installation
1. **Install Python via Homebrew**
   ```bash
   brew install python
   ```

2. **Verify Installation**
   ```bash
   python3 --version
   pip3 --version
   ```

3. **Create Virtual Environment**
   ```bash
   python3 -m venv ballbat-env
   source ballbat-env/bin/activate
   ```

#### Linux Installation
1. **Install Python**
   ```bash
   # Ubuntu/Debian
   sudo apt update
   sudo apt install python3 python3-pip python3-venv
   
   # CentOS/RHEL
   sudo yum install python3 python3-pip
   ```

2. **Verify Installation**
   ```bash
   python3 --version
   pip3 --version
   ```

3. **Create Virtual Environment**
   ```bash
   python3 -m venv ballbat-env
   source ballbat-env/bin/activate
   ```

### Browser Setup

#### Chrome/Chromium Installation

**Windows:**
1. Download Chrome from [google.com/chrome](https://google.com/chrome)
2. Install and ensure it's in your PATH

**macOS:**
1. Download Chrome from [google.com/chrome](https://google.com/chrome)
2. Or install via Homebrew: `brew install --cask google-chrome`

**Linux:**
```bash
# Ubuntu/Debian
wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | sudo apt-key add -
echo 'deb [arch=amd64] https://dl.google.com/linux/chrome/deb/ stable main' | sudo tee /etc/apt/sources.list.d/google-chrome.list
sudo apt update
sudo apt install google-chrome-stable

# CentOS/RHEL
sudo yum install google-chrome-stable
```

### ChromeDriver Setup (Automatic - Recommended)

BallBat uses `webdriver-manager` for automatic ChromeDriver management. This eliminates the need to manually download and configure ChromeDriver:

```bash
# Install webdriver-manager (included in requirements.txt)
pip install webdriver-manager

# The bot will automatically download and manage ChromeDriver
```

**Benefits of automatic installation:**
- ✅ No manual ChromeDriver downloads required
- ✅ Automatic version management and updates
- ✅ Cross-platform compatibility (Windows, macOS, Linux)
- ✅ Production-ready deployment

**How it works:**
1. On first run, webdriver-manager detects your Chrome version
2. Downloads the compatible ChromeDriver automatically
3. Manages the driver path and updates
4. Handles driver cleanup on exit

**Troubleshooting automatic setup:**
```bash
# Force reinstall of ChromeDriver
python -c "from webdriver_manager.chrome import ChromeDriverManager; ChromeDriverManager().install()"

# Check Chrome version compatibility
python -c "import selenium; print(selenium.__version__)"
```

### Manual ChromeDriver Setup (Alternative)

BallBat uses `webdriver-manager` to automatically download and manage ChromeDriver, so manual setup is usually not required. However, if you encounter issues:

#### Manual ChromeDriver Installation

1. **Download ChromeDriver**
   - Visit [chromedriver.chromium.org](https://chromedriver.chromium.org)
   - Download version matching your Chrome browser

2. **Install ChromeDriver**
   ```bash
   # Extract and move to PATH
   unzip chromedriver_linux64.zip
   sudo mv chromedriver /usr/local/bin/
   chmod +x /usr/local/bin/chromedriver
   ```

3. **Verify Installation**
   ```bash
   chromedriver --version
   ```

### Dependencies Installation

#### Core Dependencies
```bash
pip install selenium webdriver-manager pandas beautifulsoup4 requests python-dotenv
```

#### Optional Dependencies
```bash
# For notifications
pip install python-telegram-bot schedule

# For advanced data analysis
pip install numpy scipy matplotlib seaborn

# For database support
pip install sqlalchemy sqlite3

# For web interface
pip install flask fastapi uvicorn
```

#### Development Dependencies
```bash
# For testing
pip install pytest unittest-xml-reporting

# For code quality
pip install flake8 black isort mypy

# For documentation
pip install sphinx sphinx-rtd-theme
```

### Environment Configuration

#### Basic Configuration (.env)
```env
# Browser Configuration
HEADLESS=true
SELENIUM_TIMEOUT=30

# Strategy Configuration
MIN_BTTS_PERCENTAGE=60
MIN_GOALS_SCORED=1.4
MIN_GOALS_CONCEDED=1.3
H2H_THRESHOLD=60
MIN_CONFIDENCE=65

# Risk Management
MAX_BET_AMOUNT=50
BANKROLL=1000
KELLY_FRACTION=0.25

# Output Configuration
OUTPUT_FORMAT=csv
OUTPUT_DIR=outputs
```

#### Advanced Configuration
```env
# Advanced Browser Settings
CHROME_DRIVER_PATH=/path/to/chromedriver
USER_AGENT_ROTATION=true
PROXY_SERVER=proxy.example.com:8080

# Advanced Strategy Settings
LEAGUE_BTTS_THRESHOLD=55
VALUE_THRESHOLD=0.05
CONFIDENCE_WEIGHTS=0.3,0.25,0.25,0.2

# Advanced Risk Management
DAILY_LOSS_LIMIT=0.05
WEEKLY_PROFIT_TARGET=0.15
STOP_ON_LOSS_STREAK=5

# Advanced Output Settings
NOTIFICATION_ENABLED=true
TELEGRAM_BOT_TOKEN=your_token_here
TELEGRAM_CHAT_ID=your_chat_id
```

## Testing Installation

### Basic Functionality Test
```bash
python main.py --test
```

Expected output:
```
✓ Python version: 3.9.0
✓ Selenium version: 4.15.0
✓ ChromeDriver version: 120.0.6099.109
✓ Required packages installed
✓ Chrome browser accessible
✓ Test scraping successful
✓ Strategy calculation working
✓ Output generation working
```

### Full System Test
```bash
python main.py --test-full
```

This will:
1. Test browser automation
2. Scrape sample data
3. Run strategy calculations
4. Generate output files
5. Test notification system (if configured)

### Troubleshooting Common Issues

#### Chrome Not Found
```bash
# Error: Chrome not found
# Solution: Specify Chrome path in .env
CHROME_BINARY_PATH=/path/to/chrome
```

#### ChromeDriver Issues
```bash
# Error: ChromeDriver not found
# Solution: Update webdriver-manager
pip install --upgrade webdriver-manager

# Or specify manual path
CHROME_DRIVER_PATH=/path/to/chromedriver
```

#### Permission Denied
```bash
# Error: Permission denied
# Solution: Check file permissions
chmod +x main.py
chmod +x venv/bin/activate
```

#### Network Issues
```bash
# Error: Connection timeout
# Solution: Check internet connection and proxy settings
PROXY_ENABLED=false
SELENIUM_TIMEOUT=60
```

#### Memory Issues
```bash
# Error: Out of memory
# Solution: Increase timeout and reduce parallel processing
SELENIUM_TIMEOUT=120
MAX_CONCURRENT_REQUESTS=1
```

## Docker Installation (Alternative)

### Prerequisites
- Docker installed and running
- Docker Compose (for multi-container setup)

### Quick Docker Setup
```bash
# Build Docker image
docker build -t ballbat-bot .

# Run container
docker run -it --rm ballbat-bot python main.py --test
```

### Docker Compose Setup
```bash
# Start all services
docker-compose up -d

# View logs
docker-compose logs -f

# Stop services
docker-compose down
```

## Production Deployment

### Server Requirements
- **CPU**: 2+ cores
- **RAM**: 8GB+
- **Storage**: 10GB+
- **OS**: Ubuntu 20.04+ or CentOS 8+

### Production Setup
```bash
# 1. Install system dependencies
sudo apt update
sudo apt install python3 python3-pip python3-venv

# 2. Create system user
sudo useradd -m -s /bin/bash ballbat
sudo su - ballbat

# 3. Setup application
git clone https://github.com/yourusername/BallBat.git
cd BallBat
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt

# 4. Configure systemd service
sudo cp deployment/ballbat.service /etc/systemd/system/
sudo systemctl enable ballbat
sudo systemctl start ballbat
```

### Monitoring Setup
```bash
# Install monitoring tools
pip install psutil requests

# Setup log rotation
sudo cp deployment/logrotate.conf /etc/logrotate.d/ballbat
```

## Verification Checklist

- [ ] Python 3.9+ installed
- [ ] Virtual environment created and activated
- [ ] All required packages installed
- [ ] Chrome browser installed
- [ ] ChromeDriver accessible
- [ ] Environment variables configured
- [ ] Basic functionality test passed
- [ ] Full system test passed
- [ ] Output files generated correctly
- [ ] Notifications working (if configured)

## Next Steps

After successful installation:

1. **Configure your betting strategy** in `config/strategy.json`
2. **Set up your bankroll management** in `.env`
3. **Test with small amounts** before going live
4. **Monitor performance** using the logging system
5. **Consider setting up automated scheduling** using cron or task scheduler

For detailed usage instructions, see [USAGE.md](USAGE.md).

For development guidelines, see [DEVELOPMENT.md](DEVELOPMENT.md).

For troubleshooting, see [TROUBLESHOOTING.md](docs/TROUBLESHOOTING.md).