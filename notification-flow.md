# shall a notification be shown?

```

// on incoming message / reaction / webxdc-notify ...


if notifications_granted_by_system:
    if not profile_muted:
        if not chat_muted:
            DO_NOTIFY()
        else:
            if is_webxdc_notify || is_reaction_to_own_message || is_reply_to_own_message:
                if is_multiuser_chat:
                    if mentions_enabled:
                        DO_NOTIFY()


// in all other cases: do not notify
// in case the chat/app being notified is in scope, depending on UI, notification may be skipped

```
