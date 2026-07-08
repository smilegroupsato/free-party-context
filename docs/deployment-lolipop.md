# Lolipop FTP Deployment

This repository deploys only the `flyer/` directory to Lolipop via GitHub Actions.

The repository root is for context.  
The public web flyer lives in `flyer/`.

## Workflow

```text
.github/workflows/deploy-flyer.yml
```

The workflow runs when:

- files under `flyer/` are changed on `main`
- the workflow is manually triggered from GitHub Actions

## Required GitHub Secrets

Set these secrets in GitHub:

```text
LOLIPOP_FTP_HOST
LOLIPOP_FTP_USER
LOLIPOP_FTP_PASSWORD
LOLIPOP_FTP_REMOTE_DIR
```

## Where to set secrets

GitHub repository:

```text
Settings
  -> Secrets and variables
  -> Actions
  -> Repository secrets
  -> New repository secret
```

## Meaning

```text
LOLIPOP_FTP_HOST       = FTP server hostname from Lolipop
LOLIPOP_FTP_USER       = FTP account / user name from Lolipop
LOLIPOP_FTP_PASSWORD   = FTP password from Lolipop
LOLIPOP_FTP_REMOTE_DIR = remote directory for eternalfree.party
```

Example remote directory pattern:

```text
/home/users/.../web/eternalfree.party/
```

Use the exact directory shown or configured in Lolipop.

## Important

Do not commit FTP credentials to the repository.

Keep all credentials in GitHub Secrets.

## Deployment source

Only this local directory is deployed:

```text
flyer/
```

The workflow mirrors it to:

```text
$LOLIPOP_FTP_REMOTE_DIR
```

The workflow uses `mirror --reverse --delete`, so files deleted from `flyer/` may also be deleted from the remote flyer directory.

## First deployment checklist

1. Configure the domain `eternalfree.party` in Lolipop.
2. Confirm the document root / publish directory.
3. Add the four GitHub Secrets.
4. Open GitHub Actions.
5. Run `Deploy flyer to Lolipop` manually.
6. Check `https://eternalfree.party`.

## Position

```text
root = repository context
flyer/ = web flyer
eternalfree.party = published flyer
```
