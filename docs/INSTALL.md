<!--
  - SPDX-FileCopyrightText: 2024 Nextcloud GmbH and Nextcloud contributors
  - SPDX-License-Identifier: AGPL-3.0-or-later
-->
# Installation Guide

This guide will help you install the Nextcloud Assistant app on your Nextcloud instance.

## Requirements

- Nextcloud version 30 or higher (up to version 33)
- PHP and web server configured for Nextcloud
- Administrator access to your Nextcloud instance

## Installation Methods

### Method 1: Via Nextcloud App Store (Recommended)

This is the easiest and recommended method for most users:

1. Log in to your Nextcloud instance as an administrator
2. Click on your user avatar in the top-right corner
3. Select **Apps** from the dropdown menu
4. In the Apps page, select the **AI** or **Integration** category from the left sidebar
5. Find **Nextcloud Assistant** in the list
6. Click the **Download and enable** button

The app will be automatically downloaded, installed, and enabled.

### Method 2: Manual Installation from Release

If you prefer to install manually or the App Store is not available:

1. Download the latest release from the [GitHub releases page](https://github.com/nextcloud/assistant/releases)
2. Extract the archive
3. Upload the `assistant` folder to your Nextcloud `apps` directory:
   ```bash
   cp -r assistant /path/to/nextcloud/apps/
   ```
4. Set the correct permissions:
   ```bash
   chown -R www-data:www-data /path/to/nextcloud/apps/assistant
   ```
5. Enable the app using the `occ` command:
   ```bash
   sudo -u www-data php /path/to/nextcloud/occ app:enable assistant
   ```
   Or enable it from the Nextcloud web interface (Apps page)

### Method 3: Installation from Source (For Developers)

If you want to contribute or test the latest development version:

1. Clone the repository:
   ```bash
   cd /path/to/nextcloud/apps/
   git clone https://github.com/nextcloud/assistant.git
   cd assistant
   ```

2. Install dependencies and build the app:
   ```bash
   make build
   ```
   
   This will:
   - Install PHP dependencies via Composer
   - Install JavaScript dependencies via npm
   - Build the frontend assets

3. Set the correct permissions:
   ```bash
   chown -R www-data:www-data /path/to/nextcloud/apps/assistant
   ```

4. Enable the app:
   ```bash
   sudo -u www-data php /path/to/nextcloud/occ app:enable assistant
   ```

## Post-Installation Configuration

### Installing AI Providers

The Assistant app requires AI provider apps to function. You need to install at least one provider app for text processing, image generation, or speech-to-text functionality.

#### Text Processing Providers

- **[Local Large Language Model](https://github.com/nextcloud/llm2)** - Run AI models locally
- **[OpenAI/LocalAI Integration](https://apps.nextcloud.com/apps/integration_openai)** - Use OpenAI or LocalAI services

#### Image Generation Providers

- **[OpenAI/LocalAI Integration](https://apps.nextcloud.com/apps/integration_openai)**
- **[Text2Image Stable Diffusion](https://apps.nextcloud.com/apps/text2image_stablediffusion)**

#### Speech-to-Text Providers

- **[OpenAI/LocalAI Integration](https://apps.nextcloud.com/apps/integration_openai)**
- **[Local Whisper Speech-To-Text](https://apps.nextcloud.com/apps/stt_whisper)**

Install these providers from the Nextcloud App Store in the same way you installed the Assistant app.

### Verifying Installation

1. After installation, you should see a new icon in the top-right header menu (next to your user avatar)
2. Click this icon to open the Assistant interface
3. If no task types appear, you need to install and configure AI provider apps (see above)

## Troubleshooting

### App doesn't appear in the Apps list

- Ensure your Nextcloud version is between 30 and 33
- Check the Nextcloud logs for any errors: `/path/to/nextcloud/data/nextcloud.log`

### Assistant icon doesn't appear in the header

- Clear your browser cache
- Check that the app is enabled: `sudo -u www-data php occ app:list`
- Verify the app was properly built if installed from source

### No task types available

- Install at least one AI provider app (see Post-Installation Configuration above)
- Configure the provider app in Nextcloud settings

### Permission errors

Ensure the web server user (usually `www-data`, `nginx`, or `apache`) owns the app files:
```bash
chown -R www-data:www-data /path/to/nextcloud/apps/assistant
```

## Additional Resources

- [User Documentation](./user) - How to use the Assistant
- [Developer Documentation](./developer) - Integration and API documentation
- [Admin Documentation](https://docs.nextcloud.com/server/latest/admin_manual/ai/index.html) - Nextcloud AI setup
- [GitHub Issues](https://github.com/nextcloud/assistant/issues) - Report bugs or request features

## Uninstallation

To uninstall the Assistant app:

1. Via web interface: Go to Apps page, find Assistant, and click **Remove**
2. Via command line:
   ```bash
   sudo -u www-data php /path/to/nextcloud/occ app:disable assistant
   sudo -u www-data php /path/to/nextcloud/occ app:remove assistant
   ```
