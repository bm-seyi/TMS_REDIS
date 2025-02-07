##  0.0.1
first development version

## 0.0.2
### Fixed/Updated  
- Modified the [docker-build](.github/workflows/docker-build.yml) workflow to run on a GitHub-hosted runner instead of a self-hosted one.  

### Removed  
- Removed [redis](redis.conf) from [.gitignore](.gitignore) since all sensitive information has been stripped from the file and will now be added at runtime.