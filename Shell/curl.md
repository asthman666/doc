(TLS) By default, every SSL connection curl makes is verified to be secure. This option allows curl to proceed
and operate even for server connections otherwise considered insecure.

The server connection is verified by making sure the server's certificate contains the right name and verifies
successfully using the cert store.

    curl --insecure https://example.com


-s, --silent
        Silent or quiet mode. Don't show progress meter or error messages.  Makes Curl mute. It will still output the
        data you ask for, potentially even to the terminal/stdout unless you redirect it.

        Use -S, --show-error in addition to this option to disable progress meter but still show error messages.

        Example:
        curl -s https://example.com

        See also -v, --verbose, --stderr and --no-progress-meter.   

The total amount of bytes that were downloaded. This is the size of the body/data that was transfered, excluding headers.

    curl -so /dev/null https://www.amazon.com -w "%{size_download}\n"