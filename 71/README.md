# Build a new Version
```bash
docker build -t zf2timo\dev-php71 -t zf2timo\dev-php71:1.0 .
```

# Execute a PHP script
```bash
docker run -it --rm --name my-running-script -v "$PWD":/usr/src/app -w /usr/src/app zf2timo\dev-php71 php your-script.php
```

# Alias for easy use
```bash
alias docker-php71="docker run -it --rm --name my-running-script -v "$PWD":/usr/src/app -w /usr/src/app zf2timo\dev-php71 php $@"
```