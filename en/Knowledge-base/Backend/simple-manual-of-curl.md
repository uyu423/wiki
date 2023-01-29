---
title: Simple Manual of cURL
description: 
published: true
date: 2023-01-29T17:24:28.943Z
tags: 
editor: markdown
dateCreated: 2023-01-29T17:24:28.943Z
---


# Simple Manual of cURL

## What is cURL?

cURL is a command line tool for transferring data specified with URL syntax. cURL supports various protocols like, DICT, FILE, FTP, FTPS, Gopher, HTTP, HTTPS, IMAP, IMAPS, LDAP, LDAPS, POP3, POP3S, RTMP, RTSP, SCP, SFTP, SMTP, SMTPS, Telnet and TFTP. libcurl is the library curl is using to do its job.

## How to use cURL?

### Syntax

```
curl [options...] [URL...]
```

### Options

```
-a, --append              Append to target file when uploading (FTP/SFTP)
-A, --user-agent <string> Send User-Agent <string> to server
-b, --cookie <name=string/file> Read cookies from <file> (HTTP/HTTPS) or session
-B, --use-ascii           Use ASCII/text transfer
-c, --cookie-jar <file>   Write cookies to <file> after operation (HTTP/HTTPS)
-d, --data <data>         HTTP POST data (H)
-D, --dump-header <file>  Write the received headers to <file>
-e, --referer             Referer URL (H)
-E, --cert <certificate[:password]> Client certificate file and password (SSL)
-f, --fail                Fail silently (no output at all) on HTTP errors (H)
-F, --form <name=content> Specify HTTP multipart POST data (H)
-g, --globoff             Disable URL sequences and ranges using {} and []
-G, --get                 Send the -d data with a HTTP GET (H)
-h, --help                This help text
-H, --header <line>       Custom header to pass to server (H)
-i, --include             Include protocol headers in the output (H/F)
-I, --head                Show document info only
-j, --junk-session-cookies Ignore session cookies read from file (H)
-k, --insecure            Allow connections to SSL sites without certs (H)
-l, --list-only           List only mode (F/P)
-L, --location            Follow Location: hints (H)
-m, --max-time <seconds>  Maximum time in seconds that you allow the whole operation to take
-M, --manual              Display the full manual
-n, --netrc               Must read .netrc for user name and password
-N, --no-buffer           Disable buffering of the output stream
-o, --output <file>       Write output to <file> instead of stdout
-O, --remote-name         Write output to a local file named like the remote file we get
-p, --proxytunnel         Perform non-HTTP services through a HTTP proxy
-P, --ftp-port <address>  Use Active Mode FTP or SFTP on given port
-q, --disable             Disable .curlrc (must be first parameter!)
-r, --range <range>       Retrieve a byte range from a HTTP/1.1 or FTP server
-s, --silent              Silent mode. Don't output anything
-S, --show-error          Show error. With -s, make curl show errors when they occur
-t, --telnet-option <opt=val> Set telnet option
-T, --upload-file <file>  Transfer <file> to remote site
-u, --user <user[:password]> Set server user and password
-U, --proxy-user <user[:password]> Set proxy user and password
-v, --verbose             Make the operation more talkative
-V, --version             Show version number and quit
-w, --write-out <format>  Make curl display information using a specific format
-x, --proxy <proxy>       Use proxy for transfer
-X, --request <command>   Specify request command to use
-y, --speed-time <time>   Time needed to trig speed-limit abort. Defaults to 30
-Y, --speed-limit <speed> Stop transfer if below speed (bytes/sec). Defaults to 102400
-z, --time-cond <time>    Transfer if time condition is met
-0, --http1.0             Use HTTP 1.0
-1, --tlsv1               Use TLSv1 (SSL)
-2, --sslv2               Use SSLv2 (SSL)
-3, --sslv3               Use SSLv3 (SSL)
--3p-quote               Quote 3rd party headers in the output (H)
--4, --ipv4                Resolve name to IPv4 address
--6, --ipv6                Resolve name to IPv6 address
--7, --http2               Use HTTP 2 (H)
--8, --http2-prior-knowledge Require HTTP 2 knowledge on connecting end (H)
--ignore-content-length   Ignore the HTTP Content-Length header
--http2-max-streams <n>   Maximum number of concurrent streams in HTTP/2 transfers (H)
--interface <name>        Perform an operation using a specified interface. You can enter the interface name, or you can enter an IP address.
--key <key>               Private key file name (SSL/SSH)
--key-type <type>         Key file type (DER/PEM/ENG) (SSL)
--krb                      Enable Kerberos authentication (FTP)
--libcurl <file>          Dump libcurl equivalent code of this command line
--limit-rate <speed>      Limit transfer speed to this rate
--location-trusted       With -i, (HTTP/HTTPS) if the server reports that the requested page has moved to a different location (indicated with a Location: header and a 3XX response code), this option will make curl redo the request on the new place. If used together with -i, --include or -I, --head, headers from all requested pages will be shown. When authentication is used, curl only sends its credentials to the initial host. If a redirect takes curl to a different host, it won't be able to intercept the user+password. See also --location-trusted on how to change this. You can limit the amount of redirects that are followed by using the --max-redirs option.
--mail-from <address>    Mail from this address
--mail-rcpt <address>     Mail to this address
--max-filesize <bytes>    Maximum file size to download (H/F)
--max-redirs <num>        Maximum number of redirects allowed (H)
--max-time <seconds>      Maximum time allowed for the transfer
--metalink               Process given URLs as Metalink XML files
--negotiate              Use HTTP Negotiate (SPNEGO) authentication (H)
--netrc-file <file>      Specify alternative netrc file (must be first parameter!)
--netrc-optional         Use either .netrc or URL; defaults to off.
--netrc-required         Use .netrc or URL; defaults to on.
--ntlm                  Use HTTP NTLM authentication (H)
--oauth2-bearer <token>  OAuth 2 Bearer Token (IMAP, POP3, SMTP)
--proxy-anyauth          Pick "any" authentication method (H)
--proxy-basic            Use Basic authentication on the proxy (H)
--proxy-digest           Use Digest authentication on the proxy (H)
--proxy-ntlm             Use NTLM authentication on the proxy (H)
--proxy1.0 <proxyhost[:port]> Use the specified HTTP 1.0 proxy
--pubkey <key>           Public key file name (SSH)
--post301                Do not switch to GET after following a 301 redirect (H)
--post302                Do not switch to GET after following a 302 redirect (H)
--post303                Do not switch to GET after following a 303 redirect (H)
--proto <protocols>      Enable/disable specified protocols
--proto-default <protocol> Specify the default protocol (H)
--proto-redir <protocols> Enable/disable specified protocols on redirect (H)
--proxy-service-name <name> SPNEGO proxy service name
--proxy-ssl-allow-beast  Allow security flaw to be used
--proxy-tls13-ciphers <ciphersuite list> TLS 1.3 ciphersuites for proxy (OpenSSL)
--proxy-tlsauthtype <type> TLS authentication type (default: SRP)
--proxy-tlspassword <string> TLS password
--proxy-tlsuser <name>    TLS username
--proxy-tlsv1             Use TLSv1 for the proxy (H)
--proxy-tlsv1.0           Use TLSv1.0 for the proxy (H)
--proxy-t