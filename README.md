# admin
Settings for safe-settings app

# These settings are synced to GitHub by https://github.com/github/safe-settings

repositories: 
  # This is a list of repositories that need to be synced. 
  # If the repository is not listed in the settings.yml, it will still be synced once it is manually created. 

  # See https://developer.github.com/v3/repos/#edit for all available settings for a repository
  - name: new-repo
    
    # The Organization the repo belongs to
    org: github
    
    # A short description of the repository that will show up on GitHub
    description: description of the repo
  
    # A URL with more information about the repository
    homepage: https://example.github.io/
    
    # Keep this as true for most cases
    # A lot of the policies below cannot be implemented on bare repos
    auto_init: true
    
    # A comma-separated list of topics to set on the repository
    topics: github, probot, new-topic, another-topic, topic-12
  
    # Either `true` to make the repository private, or `false` to make it public. 
    private: false
  
    # Either `true` to enable issues for this repository, `false` to disable them.
    has_issues: true
  
    # Either `true` to enable projects for this repository, or `false` to disable them.
    # If projects are disabled for the organization, passing `true` will cause an API error.
    has_projects: true
  
    # Either `true` to enable the wiki for this repository, `false` to disable it.
    has_wiki: true
  
    # Either `true` to enable downloads for this repository, `false` to disable them.
    has_downloads: true
  
    # Updates the default branch for this repository.
    default_branch: main-enterprise
  
    # Either `true` to allow squash-merging pull requests, or `false` to prevent
    # squash-merging.
    allow_squash_merge: true
  
    # Either `true` to allow merging pull requests with a merge commit, or `false`
    # to prevent merging pull requests with merge commits.
    allow_merge_commit: true
  
    # Either `true` to allow rebase-merging pull requests, or `false` to prevent
    # rebase-merging.
    allow_rebase_merge: true
    
  # This is another repo
  - name: another-repo
    # Keep this as true as branch protections will not be applied otherwise
    auto_init: true
    org: github
    # A short description of the repository that will show up on GitHub
    description: description of another repo
 
# The following attributes are applied to any repo within the org
# So if a repo is not listed above is created or edited
# The app will apply the following settings to it
labels:
  # Labels: define labels for Issues and Pull Requests
  - name: bug
    color: CC0000
    description: An issue with the system

  - name: feature
    # If including a `#`, make sure to wrap it with quotes!
    color: '#336699'
    description: New functionality.

  - name: first-timers-only
    # include the old name to rename an existing label
    oldname: Help Wanted
    color: '#326699'
  - name: new-label
    # include the old name to rename an existing label
    oldname: Help Wanted
    color: '#326699'

collaborators:
# Collaborators: give specific users access to any repository.
# See https://developer.github.com/v3/repos/collaborators/#add-user-as-a-collaborator for available options

- username: regpaco
  permission: push
# Note: Only valid on organization-owned repositories.
# The permission to grant the collaborator. Can be one of:
# * `pull` - can pull, but not push to or administer this repository.
# * `push` - can pull and push, but not administer this repository.
# * `admin` - can pull, push and administer this repository.

# See https://developer.github.com/v3/teams/#add-or-update-team-repository for available options
teams:
  - name: core
    # The permission to grant the team. Can be one of:
    # * `pull` - can pull, but not push to or administer this repository.
    # * `push` - can pull and push, but not administer this repository.
    # * `admin` - can pull, push and administer this repository.
    permission: admin
  - name: docss
    permission: push
  - name: docs
    permission: pull

branches:
  # If the name of the branch is default, it will create a branch protection for the default branch in the repo
  - name: default
    # https://developer.github.com/v3/repos/branches/#update-branch-protection
    # Branch Protection settings. Set to null to disable
    protection:
      # Required. Require at least one approving review on a pull request, before merging. Set to null to disable.
      required_pull_request_reviews:
        # The number of approvals required. (1-6)
        required_approving_review_count: 1
        # Dismiss approved reviews automatically when a new commit is pushed.
        dismiss_stale_reviews: true
        # Blocks merge until code owners have reviewed.
        require_code_owner_reviews: true
        # Specify which users and teams can dismiss pull request reviews. Pass an empty dismissal_restrictions object to disable. User and team dismissal_restrictions are only available for organization-owned repositories. Omit this parameter for personal repositories.
        dismissal_restrictions:
          users: []
          teams: []
      # Required. Require status checks to pass before merging. Set to null to disable
      required_status_checks:
        # Required. Require branches to be up to date before merging.
        strict: true
        # Required. The list of status checks to require in order to merge into this branch
        contexts: []
      # Required. Enforce all configured restrictions for administrators. Set to true to enforce required status checks for repository administrators. Set to null to disable.
      enforce_admins: true
      # Required. Restrict who can push to this branch. Team and user restrictions are only available for organization-owned repositories. Set to null to disable.
      restrictions:
        apps: []
        users: []
        teams: []
        

