# Laravel Deploy Action

This GitHub Action deploys a Laravel project to a server via FTP, with customizable PHP versions and extensions.

## Inputs

- `branch`: The branch to deploy. This input determines which branch (production or development) will be deployed.
- `php-version`: PHP version to use (default: 8.1). You can specify any PHP version supported by the `shivammathur/setup-php` action.
- `php-extensions`: Comma-separated list of PHP extensions to install (default: "mbstring,xml,intl,curl,gd"). Modify this list according to your project's requirements.
- `ftp-username-main`: FTP username for the main branch. This should be the username used for production deployments.
- `ftp-username-dev`: FTP username for the development branch. This should be the username used for development deployments.
- `ftp-server`: FTP server address. This is the FTP server where your Laravel project will be deployed.
- `ftp-password`: FTP password. This is the password used for FTP deployment.
- `use-env-files`: Whether to use `.env.prod` and `.env.dev` files (default: true). If set to true, the action will copy `.env.prod` for production and `.env.dev` for development. If false, the action will use `.env.example`.

## Usage

### Example Workflow

```yaml
name: Deploy to Server
on: push
jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v2
      - name: Deploy
        uses: your-username/laravel-deploy-action@v1
        with:
          branch: ${{ github.ref_name }}
          php-version: '8.1'
          php-extensions: 'mbstring,xml,intl,curl,gd'
          ftp-username-main: 'your-main-username'
          ftp-username-dev: 'your-dev-username'
          ftp-server: 'ftp.yourserver.com'
          ftp-password: 'your-ftp-password'
          use-env-files: 'true'
```

### Acknowledgments

This GitHub Action leverages several other amazing GitHub Actions:

- **[actions/checkout](https://github.com/actions/checkout)**: Used to check out the repository code.
- **[shivammathur/setup-php](https://github.com/shivammathur/setup-php)**: Used to set up the desired PHP version and extensions.
- **[SamKirkland/FTP-Deploy-Action](https://github.com/SamKirkland/FTP-Deploy-Action)**: Used to sync files via FTP to the server.

These tools make it easy to build and deploy your Laravel applications in a continuous integration/continuous deployment (CI/CD) pipeline.
