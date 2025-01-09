# Code Synchronization Configuration Guide

This project supports automatic code synchronization to multiple code hosting platforms (such as Gitee, GitCode, Coding, etc.).

## 1. Configuration Steps

### 1.1 Configure GitHub Secrets

1. Go to Settings -> Secrets and variables -> Actions in your GitHub repository
2. Click "New repository secret"
3. Name: `SYNC_CONFIG`
4. Value should contain the following configuration:

```yaml
# Code sync configuration
repositories:
  gitee:  # Platform identifier
    enabled: true  # Enable sync
    username: your-gitee-username  # Platform username
    repo: your-repo-name  # Repository name
    token: your-gitee-token  # Access token
    domain: gitee.com  # Platform domain
    
  gitcode:
    enabled: true
    username: your-gitcode-username
    repo: your-repo-name
    token: your-gitcode-token
    domain: gitcode.com
    
  coding:
    enabled: false  # Set false to temporarily disable sync for a platform
    username: your-coding-username
    repo: your-coding-repo-path
    token: your-coding-token
    domain: e.coding.net
```

## 2. Obtaining Access Tokens

### 2.1 Chinese Platforms

#### Gitee
1. Visit https://gitee.com/profile/personal_access_tokens
2. Click "Generate new token"
3. Select "repo" permission
4. Generate and copy token

#### GitCode (CSDN)
1. Visit https://gitcode.net/-/profile/personal_access_tokens
2. Set token name and expiration
3. Select "api", "read_repository", "write_repository" permissions
4. Click create and save token

#### Coding (Tencent)
1. Visit https://coding.net/user/account/setting/tokens
2. Click "New access token"
3. Select "project:depot" permission
4. Create and copy token

#### JiHuLab
1. Visit https://jihulab.com/-/profile/personal_access_tokens
2. Set token name and expiration
3. Select "api", "read_repository", "write_repository" permissions
4. Create token

#### Alibaba Cloud Code
1. Visit https://codeup.aliyun.com/profile/personal-access-tokens
2. Click "Create personal access token"
3. Select repository read/write permissions
4. Create and save token

### 2.2 International Platforms

#### GitLab
1. Visit https://gitlab.com/-/profile/personal_access_tokens
2. Set token name and expiration
3. Select "api", "read_repository", "write_repository" permissions
4. Create token

#### Bitbucket
1. Visit https://bitbucket.org/account/settings/app-passwords/
2. Click "Create app password"
3. Select "Repository Read" and "Repository Write" permissions
4. Create and save password

#### Azure DevOps
1. Visit https://dev.azure.com/YOUR-ORG/_usersSettings/tokens
2. Click "New Token"
3. Select "Code (Read & Write)" permission
4. Create and save token

#### AWS CodeCommit
1. Visit https://console.aws.amazon.com/iam/home#/security_credentials
2. Go to "HTTPS Git credentials for AWS CodeCommit" section
3. Click "Generate credentials"
4. Download and save credentials

#### Google Cloud Source
1. Visit https://source.cloud.google.com/user/settings/tokens
2. Click "Create token"
3. Set permission scope
4. Create and save token

Important Notes:
1. Save tokens immediately after creation, most platforms only display them once
2. Set appropriate expiration times
3. Select only necessary minimum permission scopes
4. Regularly check and update tokens

## 3. Sync Triggers

Code synchronization will be automatically triggered in the following cases:

1. When pushing to main branch
2. When manually triggering the workflow

### 3.1 Manual Trigger Steps
1. Visit repository's Actions page
2. Select "Sync to Multiple Repositories" workflow
3. Click "Run workflow"
4. Select main branch and confirm

## 4. Important Considerations

1. **Security**
   - Don't commit sync-config.yml file containing sensitive information
   - Ensure it's added to .gitignore
   - Only configure through GitHub Secrets

2. **Token Permissions**
   - Ensure tokens have sufficient permissions (at least repository read/write access)
   - Recommend rotating tokens periodically
   - Revoke tokens immediately if compromised

3. **Repository Settings**
   - Target repository must exist
   - Ensure username and repository names are correct
   - Verify domain configuration

4. **Sync Behavior**
   - Sync will force override target repository content
   - Includes all branches and tags
   - Recommend using target repositories only for sync, not direct development

## 5. Troubleshooting

### 5.1 Common Issues

1. Sync Failure
   - Check if token is valid
   - Verify repository path
   - Confirm username is correct

2. Invalid Configuration
   - Validate YAML format
   - Check indentation
   - Ensure all required fields are configured

3. Permission Issues
   - Check token permission scope
   - Verify repository access permissions
   - Confirm token hasn't expired

### 5.2 Viewing Logs

1. Visit GitHub Actions page
2. Click failed workflow run
3. Expand failed steps to view detailed logs

## 6. Configuration Examples

### 6.1 Minimal Configuration (Single Platform)
```yaml
repositories:
  gitee:
    enabled: true
    username: your-username
    repo: your-repo
    token: your-token
    domain: gitee.com
```

### 6.2 Complete Configuration (Multiple Platforms)
```yaml
repositories:
  gitee:
    enabled: true
    username: gitee-username
    repo: blog-mirror
    token: gitee-token
    domain: gitee.com
    
  gitcode:
    enabled: true
    username: gitcode-username
    repo: blog-mirror
    token: gitcode-token
    domain: gitcode.com
    
  coding:
    enabled: true
    username: coding-username
    repo: blog-mirror
    token: coding-token
    domain: e.coding.net
```

## 7. Supported Platform Domains

Here are the domain configurations for common code hosting platforms:

### 7.1 Chinese Platforms
```yaml
# Gitee
domain: gitee.com

# GitCode (CSDN)
domain: gitcode.com

# Coding (Tencent)
domain: e.coding.net

# JiHuLab
domain: jihulab.com

# Alibaba Cloud Code
domain: codeup.aliyun.com

# GitLink
domain: gitlink.org.cn

# GitChina
domain: gitchina.org
```

### 7.2 International Platforms
```yaml
# GitHub
domain: github.com

# GitLab
domain: gitlab.com

# Bitbucket
domain: bitbucket.org

# Azure DevOps
domain: dev.azure.com

# AWS CodeCommit
domain: git-codecommit.{region}.amazonaws.com

# Google Cloud Source
domain: source.developers.google.com
```

Important Notes:
1. Repository path formats may differ between platforms
2. Some platforms may require special authentication methods
3. Test repository access permissions before configuring sync
4. Some platforms may have API rate limits

Recommendations:
- Prioritize platforms with stable access
- Confirm platform supports Git protocol
- Verify domain accessibility
- Check if platform supports token authentication



