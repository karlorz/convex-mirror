# convex-mirror

Mirror public Docker images from GHCR.io to Docker Hub using GitHub Actions.

## Setup

### 1. Configure Docker Hub Secrets

Add the following secrets to your GitHub repository (Settings → Secrets and variables → Actions):

- `DOCKERHUB_USERNAME`: Your Docker Hub username
- `DOCKERHUB_TOKEN`: Your Docker Hub access token (create one at https://hub.docker.com/settings/security)

### 2. Run the Workflow

#### Manual Trigger (Recommended)

Go to **Actions** → **Mirror GHCR Image to Docker Hub** → **Run workflow**

Provide:
- **Source image**: The GHCR image to mirror (e.g., `ghcr.io/owner/repo:tag`)
- **Target image**: The Docker Hub destination (e.g., `yourusername/repo:tag`)

#### Scheduled Run (Optional)

Uncomment the `schedule` section in `.github/workflows/mirror-image.yml` to run automatically.

## Workflows

### 1. Mirror Convex Backend (Recommended)

Pre-configured workflow for mirroring Convex backend images to `karlorz/convex-mirror`:
- **Latest tag**: `ghcr.io/get-convex/convex-backend:latest`
- **SHA tag**: `ghcr.io/get-convex/convex-backend:6efab6f2b6c182b90255774d747328cfc7b80dd9`

**Automatic Schedule**: Runs every Sunday at 2 AM UTC to keep images updated.

**Manual Trigger:**
1. Go to Actions → Mirror Convex Backend → Run workflow
2. Optionally change Docker Hub repository (default: `karlorz/convex-mirror`)
3. Choose whether to mirror the SHA tag
4. Click "Run workflow"

Both tags will be mirrored to your Docker Hub repository.

### 2. Mirror Any GHCR Image

Generic workflow for mirroring any GHCR image:

1. Go to Actions → Mirror GHCR Image to Docker Hub → Run workflow
2. Set source: `ghcr.io/owner/repo:tag`
3. Set target: `yourname/repo:tag`
4. Click "Run workflow"

## How It Works

The workflow:
1. Pulls the specified image from GHCR.io
2. Re-tags it for Docker Hub
3. Pushes it to your Docker Hub repository
4. Cleans up local images

No authentication is needed for pulling public GHCR images.

