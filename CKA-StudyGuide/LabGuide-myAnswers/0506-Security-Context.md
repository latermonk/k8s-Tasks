#  securityContext

```
k explain pods.spec.securityContext --recursive 
```


```
KIND:     Pod
VERSION:  v1

RESOURCE: securityContext <Object>

DESCRIPTION:
     SecurityContext holds pod-level security attributes and common container
     settings. Optional: Defaults to empty. See type description for default
     values of each field.

     PodSecurityContext holds pod-level security attributes and common container
     settings. Some fields are also present in container.securityContext. Field
     values of container.securityContext take precedence over field values of
     PodSecurityContext.

FIELDS:
   fsGroup	<integer>
   runAsGroup	<integer>
   runAsNonRoot	<boolean>
   runAsUser	<integer>
   seLinuxOptions	<Object>
      level	<string>
      role	<string>
      type	<string>
      user	<string>
   supplementalGroups	<[]integer>
   sysctls	<[]Object>
      name	<string>
      value	<string>
   windowsOptions	<Object>
      gmsaCredentialSpec	<string>
      gmsaCredentialSpecName	<string>

```

