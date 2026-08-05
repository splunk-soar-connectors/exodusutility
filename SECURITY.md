# Security considerations

## Support status

Exodus is a community-maintained connector published by its community author. It
is not developed, maintained, or officially supported by Splunk. Deployment
owners are responsible for reviewing the connector, deciding whether its trust
model is appropriate, and operating it securely.

## Asset-migration risk

Exodus is designed to migrate configuration data between SOAR instances. When an
asset contains password-typed configuration fields, the migration flow decrypts
those values on the SOAR host running Exodus and sends the resulting plaintext to
the configured target SOAR REST endpoint. The target SOAR instance then stores
the received values using its own encryption controls.

This behavior is required to preserve automatic asset migration across instances
that do not share an encryption key. It also creates a high-trust boundary:

- The source and target URLs and API tokens determine where protected
  configuration data is read and written.
- A user who can alter the Exodus asset or influence the migration responses may
  be able to redirect or expose migrated credentials.
- Disabling server-certificate verification permits interception or impersonation
  of a configured SOAR endpoint.
- API tokens used for migration may grant broad access to playbooks, custom code,
  apps, assets, or containers.
- Plaintext credentials may exist briefly in connector memory and may be exposed
  by unsafe debugging, logging, diagnostics, or host compromise.

By enabling password-bearing asset migration, the deployment owner accepts these
risks.

## Required compensating controls

Deploy Exodus only when all of the following controls are in place:

1. Restrict connector installation, asset creation and editing, ingestion, and
   migration approval to a dedicated trusted administrator or migration role.
2. Prevent Asset Owners and other untrusted users from modifying the Exodus asset,
   triggering its ingestion, or approving its migration containers.
3. Constrain source and target connectivity to explicitly approved SOAR hosts with
   firewall, proxy, or other network policy. Do not rely only on user-editable URL
   fields as a trust boundary.
4. Keep `verify_server_cert` enabled and use certificates trusted by the host
   running Exodus.
5. Use separate, narrowly scoped API tokens for source and target operations.
   Store and rotate them according to the organization's credential policy.
6. Restrict access to the `exodus` label and protect any playbook that creates or
   approves migration requests from unauthorized modification.
7. Avoid logging asset configuration data. Restrict access to connector logs,
   diagnostics, process memory, and the host filesystem.
8. Monitor migrations and configuration changes. Rotate API tokens and migrated
   credentials after any suspected endpoint redirection, unauthorized migration,
   or host compromise.

Do not enable asset migration if these controls cannot be enforced. Playbook and
custom-function migration can be used independently when password-bearing asset
migration is outside the deployment's accepted risk.

## Reporting security concerns

Because this connector is community-maintained, coordinate fixes with the
community maintainer through this repository. Do not send credentials, tokens,
or sensitive configuration data in public issues or pull requests.
