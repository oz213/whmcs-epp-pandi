# PANDI EPP with DNSsec Registrar Module for WHMCS
PANDI EPP with DNSsec Registry-Registrar Module for WHMCS >= 7.7.1

	# PANDI EPP module for WHMCS which provide full functionality coverage for domains management and based on communication with Registry through Extensible Provisioning Protocol (EPP).
	# EPP: RFC 5730, 5731, 5732, 5733, 5734, 5910


## Installation steps
	# Upload via FTP the 'pandiepp' directory to <whmcs_root>/modules/registrars/
	# Set write permissions for log file <whmcs_root>/modules/registrars/pandiepp/log/pandiepp.log



## Upload certificates
	# Copy certificate.pem to <whmcs_root>/modules/registrars/pandiepp/local_cert/certificate.pem

## Test connection with the server
	# please make sure port 700 is not firewalled:
	telnet epp-ote.id 700 
	openssl s_client -showcerts -connect epp-ote.id:700 

	# command line for acceptable client certificate CA names 
	openssl s_client -showcerts -connect epp-ote.id:700 -CAfile gd_bundle.crt

	# command line to verify your own Certificate 
	openssl s_client -showcerts -connect epp-ote.id:700 -CAfile CA_bundle.crt -cert yourdomain.id.crt -key yourdomain.id.key


## Add your whois server to the list, if not exist
	# edit file <whmcs_root>/resources/domains/dist.whois.json
	# check Not available text response on the whois server (No match for)
	,
    {
        "extensions": ".id,.co.id",
        "uri": "socket://whois.id",
        "available": "No match for"
    }


## Configure PANDI EPP module in WHMCS
	# Login to WHMCS admin panel.
	# Go to Setup > Products/Service > Domain registrars
	# Activate PANDI EPP module
	# Configure module by providing EPP Server access credentials


## Start using module
	# Login to WHMCS admin panel.
	# Go to Setup > Products/Service > Domain pricing
	# Create ".yourtld" TLD and selectg "Pandiepp" module in "Auto Registration" field
	# Define your pricing for different registration/renewal terms
