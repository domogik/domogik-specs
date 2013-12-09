||__Created:__|xx/xx/2011
__Creator:__|Ferllings
__Reviewers:__|
__Status:__|{GAUGE(value=>10, max=>100, label=>''draft'', perc=>true, labelsize=>50, height=>20, color=>green, bgcolor=>#EEEEEE)}{GAUGE}
__Target:__|0.x.0
__References:__|((Database_ui_terminal|Database Model))||

************************
 Terminals registration
************************

In order to identify a terminal and record its parameters, each terminal need to be registered the first time it connects the IHM.

When connecting the IHM for the first time:
# The terminal will ask for a registration key.
# The IHM will will ask for authorization in order to register the terminal. (directly from the terminal, by asking admin password; or from the admin pages)
# The terminal will receive the registration key

When connecting the IHM when already registered:
# The terminal will send its registration key, in order to validate his access.