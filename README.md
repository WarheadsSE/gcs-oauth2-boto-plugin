# gcs-oauth2-boto-plugin

gcs-oauth2-boto-plugin is a Python application whose purpose is to behave as
an auth plugin for the [boto] auth plugin framework for use with [OAuth 2.0]
credentials for the Google Cloud Platform. This plugin is compatible with
both [user accounts] and [service accounts], and its functionality is
essentially a wrapper around the oauth2client package of
[google-api-python-client] with the addition of automatically caching tokens
for the machine in a thread- and process-safe fashion.

For more information about how to use this plugin to access Google Cloud Storage
via boto in your application, see the [GCS documentation].

If you wish to use this plugin without using the PyPI install as instructed in
the documentation (e.g., for development), then you will need to manually
acquire the modules from the requirements.txt file.


When using this plugin, you must specify a client ID and secret. We offer the
following methods for providing this information; if multiple methods are used,
we will choose them in the following order:

1. .boto config, if not set
2. environment variables (OAUTH2_CLIENT_ID and OAUTH2_CLIENT_SECRET), if not set
3. CLIENT_ID and CLIENT_SECRET values set by SetFallbackClientIdAndSecret function.


The default locking mechanism used is threading.Lock. You can switch to using
another locking mechanism by calling SetLock. Example:

```
SetLock(multiprocessing.Manager().Lock())
```


Before submitting any code, please run the tests (e.g., by running the following
command from the root of this repository):
  PYTHONPATH="." python -m gcs_oauth2_boto_plugin.test_oauth2_client

[boto]: https://github.com/boto/boto
[OAuth 2.0]: https://developers.google.com/accounts/docs/OAuth2Login
[user accounts]: https://developers.google.com/accounts/docs/OAuth2#installed
[service accounts]: https://developers.google.com/accounts/docs/OAuth2#serviceaccount
[google-api-python-client]: https://code.google.com/p/google-api-python-client/wiki/OAuth2Client
[GCS documentation]: https://developers.google.com/storage/docs/gspythonlibrary
