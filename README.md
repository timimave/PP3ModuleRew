# ```javaPP3 Module Rew```
# Что такое Spring Security?
Spring Security это Java/Java EE фреймворк, предоставляющий механизмы построения систем аутентификации и авторизации с помощью Spring Framework.

 Ключевые объекты контекста Spring Security:
* `SecurityContextHolder`, в нем содержится информация о текущем контексте безопасности приложения, который включает в себя подробную информацию о пользователе(Principal) работающем в настоящее время с приложением. По умолчанию SecurityContextHolder используетThreadLocal для хранения такой информации, что означает, что контекст безопасности всегда доступен для методов исполняющихся в том же самом потоке. Для того что бы изменить стратегию хранения этой информации можно воспользоваться статическим методом класса SecurityContextHolder.setStrategyName(String strategy). Более подробно SecurityContextHolder
* `SecurityContext`, содержит объект Authentication и в случае необходимости информацию системы безопасности, связанную с запросом от пользователя.
* `Authentication` представляет пользователя (Principal) с точки зрения Spring Security.
* `GrantedAuthority` отражает разрешения выданные пользователю в масштабе всего приложения, такие разрешения (как правило называются «роли»), например ROLE_ANONYMOUS, ROLE_USER, ROLE_ADMIN.
* `UserDetails` предоставляет необходимую информацию для построения объекта Authentication из DAO объектов приложения или других источников данных системы безопасности. Объект UserDetailsсодержит имя пользователя, пароль, флаги: isAccountNonExpired, isAccountNonLocked, isCredentialsNonExpired, isEnabled и Collection — прав (ролей) пользователя.
* `UserDetailsService`, используется чтобы создать UserDetails объект путем реализации единственного метода этого интерфейса   
```java 
- UserDetails loadUserByUsername(String username) throws UsernameNotFoundException;
```
Позволяет получить из источника данных объект пользователя и сформировать из него объект UserDetails который будет использоваться контекстом Spring Security.

# Расспросить про конфигурацию (permitAll, authorised и т.д.)
authorised

 antMatcher(“/service”) сопоставляет путь запроса только с “/service”, в то время как mvcMatcher(“/service”) сопоставляет с “/service”, “/service.html”, “/service.abc”.
permitAll - устанавливает разрешения на доступ к определенным адресам

```java .antMatchers("/", "/index").permitAll()
.antMatchers("/api/admin/**").access("hasAnyAuthority('ADMIN')") ```
