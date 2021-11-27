# problems

record some of common problems when debugging kernel


1. `No rule to make target 'debian/canonical-certs.pem', needed by 'certs/x509_certificate_list'` 
    solution: **delete the content in `.config` about `CONFIG_SYSTEM_TRUSTED_KEYS=""` **
