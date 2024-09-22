# [Lightning Address](https://github.com/lnurl/luds/blob/luds/16.md)
If you run your own lightning node, and would like to have a lightning address to it, Bitagent can provide you one.  
Bitagent lightning addresses have the ending `@bitagent.ch`.  
So you can have an lightning address `yourname@bitagent.ch` for example.

## Configuration
To configure your lightning node Bitagent needs some data from you.

### LND
Data | Description | Example
--- | --- | ---
Host | The host as a https onion address | `https://abc:xyz.onion`
Port | The rest port of the host | `8080`
Macaroon | A macaroon with `Create/Get Invoices` permissions in base64 format | `ABC:123:xyz==`
Email (optional) | If you like to have email notifications for new invoices and wheter they are settled or canceled, you may provide an email address | `yourname@yourdomain.com`

### Other lightning nodes
The configuration of other lightning implementations is possible after consultation.

[/](./../readme.md)
