### Creating a Cloudflare API Token

To use the Cloudflare DNS challenge provider, you'll need to create an API token in your Cloudflare account. Follow these steps to create a token with the necessary permissions:

1. **Log in to Cloudflare**:
   - Go to the Cloudflare dashboard at [dash.cloudflare.com](https://dash.cloudflare.com) and log in with your account credentials.

2. **Navigate to API Tokens**:
   - Click on your profile icon in the top right corner of the dashboard.
   - Select "My Profile" from the dropdown menu.
   - In the left sidebar, click on "API Tokens".

3. **Create a Custom Token**:
   - Click the "Create Token" button.
   - Under the "Custom Token" section, click "Get started".

4. **Configure Token Permissions**:
   - Give your token a name, such as "Caddy DNS-01 Challenge".
   - Set the permissions as follows:
     - **Zone - Zone - Read**: Allows the token to Read DNS Zones
     - **Zone - DNS - Edit**: Allows the token to edit DNS records, which is required for the DNS-01 challenge.

5. **Specify Account and Zone Resources**:
   - Under "Zone Resources", set the following:
     - **Include - All Zones**: If you want the token to work with all your zones.
     - **Include - Specific Zone**: Select the specific zone(s) you want the token to have access to.

6. **Create and Store the Token**:
   - Click the "Continue to summary" button.
   - Review your token settings and click "Create Token".
   - Copy the generated token and store it in a secure place. You will need this token to set up the environment variable in your Caddy configuration.
