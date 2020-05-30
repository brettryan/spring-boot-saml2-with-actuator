
# SAML2 with Actuator

This repo serves to help others that may have found security configurations in
`application.yml` were being ignored when actuator was being used. This comes
into play as the actuator configuration will forcefully enable its own
configuration if you do not have your own `WebSecurityConfigurerAdapter` on
the classpath.

The fix is to exclude actuators `ManagementWebSecurityAutoConfiguration`on
your application.

```java
@SpringBootApplication(
        exclude = {ManagementWebSecurityAutoConfiguration.class}
)
```

As this was lifted from the SAML2 example provided by Spring it caused me to
drink heavily wondering why I couldn't integrate SAML2 into my application
yet the sample was bare bones and worked. This led me to painfully disable
dependencies tracking it down to the actuator and it's auto-configuration
rules.

