# Session Cache 

## Description

Session Cache is a Python package that provides a simple and efficient way to store and manage cached data for a session. It allows users to cache data during a session and automatically clean up expired data at regular intervals.

## Utility

Session Cache is useful for scenarios where temporary data storage is required within a session, such as web applications, API caching, or any situation where quick access to cached data is needed.

## Install

You can install the `session-cache` package via pip:

```bash
pip install ran-cache
```

## Examples of Basic Uses

```py
from scache import SessionCache as Cache
from time import sleep

# Create a session cache with default settings (ttl=1 hour, cleanup_interval=2.5 hours)
# If 'cleanup_config' is an integer > 0, automatic cleanup is started automatically
cache = Cache() # default_ttl=3600, cleanup_config=9000 

# Add data to the cache with default_ttl
cache.update('default_ttl', cache.default_ttl)

# Add data to the cache with custom ttl
cache.update('custom_ttl', 'custom', ttl=4) # 4 seconds

# Add data to the cache without ttl
cache.update('persistent_data', 'persistent', ttl=None)

# Retrieve cached values
default_ttl = cache.get("default_ttl")
custom_ttl  = cache.get("custom_ttl")

print(default_ttl) # Returns 3600 
print(custom_ttl) # Returns "custom"

sleep(4) 

# Check cached values after expiration
default_ttl = cache.get("default_ttl")
custom_ttl  = cache.get("custom_ttl")

print(default_ttl) # Returns 3600 
print(custom_ttl) # Returns None

# Change default_ttl
cache.default_ttl = 2

# Check if automatic cleanup is enabled
print(cache.cleaning_enabled) # Returns True

# Stop automatic cleanup
cache.stop_cleanup()
print(cache.cleaning_enabled) # Returns False

# Start automatic cleanup 
cache.start_cleanup()
print(cache.cleaning_enabled) # Returns True

# Automatic cleanup interval
print(cache.cleanup_config) # Returns 9000

# Change automatic cleanup interval to 1 minute
cache.cleanup_config = 60
print(cache.cleanup_config) # Returns 60

# Update a cached value and apply Default TTL (2 seconds)
cache.update("default_ttl", "new_value")

print(cache.get("default_ttl")) # Returns "new_value"

sleep(2)

print(cache.get("default_ttl")) # Returns None
```

## Contact

For any inquiries or feedback regarding this project, please contact us on [Discord](https://discord.gg/mjjzur9gBR)