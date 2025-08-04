# Telegram Gifts Buyer

Automated Telegram userbot for purchasing gifts with smart prioritization and balance management.

## Features

- Automated monitoring for new gifts
- Smart prioritization of rare gifts
- Multi-recipient support
- Intelligent balance management
- Detailed notifications
- Multi-language support (EN/RU)

## Installation

pip install -r requirements.txt

Edit `config.ini` with your settings and run:

python main.py

## Docker Usage

### Build and run for authorization (one-time setup)

docker compose build
docker compose run --rm telegram-bot

Follow the prompts to complete Telegram authorization.

### Start the bot

docker compose up -d

### Stop the bot

docker compose down

## Configuration

### Basic Settings
ini
[Telegram]
API_ID = your_api_id
API_HASH = your_api_hash
PHONE_NUMBER = +1234567890
CHANNEL_ID = -100xxxxxxxxx

[Bot]
INTERVAL = 10
LANGUAGE = EN

[Gifts]
GIFT_RANGES = 1-1000: 500000 x 1: @user1, 123456; 1001-5000: 100000 x 2: @channel
PURCHASE_ONLY_UPGRADABLE_GIFTS = False
PRIORITIZE_LOW_SUPPLY = True

### Gift Ranges Format

**Format**: `min_price-max_price: supply_limit x quantity: recipients`

**Examples**:
- `1-1000: 500000 x 1: @johndoe, 123456789` - Cheap gifts, 1 copy each
- `1001-5000: 100000 x 2: @channel, @user` - Mid-range, 2 copies each
- `5001-50000: 50000 x 5: 987654321` - Expensive gifts, 5 copies

**Recipients can be**:
- Usernames: `@username`
- User IDs: `123456789`
- Channel names: `@channelname`

## How It Works

1. Bot checks for new gifts every `INTERVAL` seconds
2. Filters gifts matching your price ranges and supply limits
3. Prioritizes rarest gifts first (if enabled)
4. Buys specified quantity for each recipient
5. Makes partial purchases if balance is insufficient

## Balance Management

The bot calculates affordable quantities before purchase:

Example:
- Gift costs 1500⭐, want to buy 4 copies
- Current balance: 4500⭐
- Result: Buys 3 copies, reports missing 1500⭐ for the last one

## Tips

- Keep balance 2-3x higher than your most expensive range
- Use multiple ranges for different strategies
- Enable notifications to monitor activity
- Test with small ranges first
- Run on VPS for 24/7 operation