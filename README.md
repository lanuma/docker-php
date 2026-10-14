# Docker php

PHP Images Optimized for CI / CD Pipeline Based on Alpine Linux

## Usage 
### docker pull
```
docker pull lanuma/php:tag
```

Available tags: `8.0`, `8.1`, `8.2`, `8.3`, `8.4`, `8.5` (`latest` = `8.5`)


Package included:

- composer 2
- git
- openssh-client
- deployer (7.5.12 for 8.0 - 8.2, 8.0.5 for 8.3+)

Php extenstion:

- gd
- mysqli 
- pdo 
- pdo_mysql 
- zip 
- mbstring 
- iconv 
- dom
- pcntl (8.1+)
