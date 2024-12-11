# shall a notification be shown?

```

// on incoming message / reaction / webxdc-mention ...


if notifications_granted_by_system:
    if not profile_muted:
        if not chat_muted:
            DO_NOTIFY()
        else:
            if is_webxdc_mention || is_reaction || is_reply_to_own_message:
                if is_group:
                    if mentions_enabled:
                        DO_NOTIFY()


// in all other cases: do not notify
// in case the chat/app being notified is in scope, depending on UI, notification may be skipped

```
