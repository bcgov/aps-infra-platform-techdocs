# JWT Keycloak

## Example

```
services:
- name: MY_REST_API
  tags: [ _NS_ ]
  plugins:
  - name: jwt-keycloak
    tags: [ _NS_ ]
    enabled: true
    config:
      well_known_template: https://keycloak/auth/realms/REALM/.well-known/openid-configuration
      allowed_iss:
      - https://keycloak/auth/realms/REALM
      run_on_preflight: true
      iss_key_grace_period: 60
      maximum_expiration: 0
      claims_to_verify:
      - exp
      cookie_names: []
      uri_param_names: []
      scope: null
      realm_roles: null
      client_roles: null
      anonymous: null
      algorithm: RS256
      consumer_match: true
      consumer_match_claim: azp
      consumer_match_ignore_not_found: false
      consumer_match_claim_custom_id: false

```