
## Requirements

Exodus migrates playbooks, custom functions, and assets via Phantom's rest API and uses containers
under an **exodus** label to specify content that is being reviewed for migration. Several things
are requires to effectively make this process flow work. You can run exodus from either your dev or
your prod instance. The chosen host is where you will configure Exodus assets and "ingestion".
Exodus does not technically ingest anything but the ingestion scheduling is used to define the
interval time between checks for now content to be migrated  

### API Tokens

You will need a Phantom API token for both your dev and your production environment  
Dev Permissions: Playbooks: R, Custom Code: RW, Apps: R, Assets: R  
Prod Permissions: Playbooks: R, Custom Code: RW, Apps: R, Assets: R  
Additional permissions for exodus ingestion host: Container: RW, Assets: W, Playbooks: W  
  

### File System

During migration, playbook and custom function tarballs are temporarily written to /tmp on the
filesystem  
  

### Label

This app creates containers under the label **exodus** . This label should be created in your
Phantom host that will run exodus. Permissions for this label should be restricted to roles that are
authorized to review and approve content for production  
  

### Tag

Exodus identifies "new" content for migration based on 2 things: object ID and tags. Any playbook
that has a new ID (because it has been changed) and a **prod** tag will be considered a candidate
for migration. The **prod** tag should be created in your dev phantom environment for this
purpose.  
  

### Playbooks and Custom Functions

Exodus identifies candidate playbooks and custom functions and creates **exodus** containers. Once
these containers are created, the only requirement left to signal Exodus to move the content to prod
is to run the Exodus action **add approval** . The methodology for how that action is invoked and
what the process looks like is defined by the organization. It can be as simple as requiring leads
on the dev team to review all new exodus containers and manually run the add approval action if they
approve or close the container if they don't approve. It is recommended that an active playbook be
created for the exodus containers that builds and sends an approval request via prompts, slack,
email, etc in order to make your process smoother and more auditable. It would be wise to store
these playbooks in an "admin" repo to prevent unauthorized users from adversly modifying the
approval process playbook.  
  

### Assets

If assets are to be migrated, exodus must be executed on the source host that the assets are
initially created on in order to stay intact.  
If assets are "pulled" from their host instead of "pushed" pasword fields will be broken.  
  
