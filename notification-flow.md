# shall a notification be shown?

```

if notifications_granted_by_system:
    if not profile_muted:
        if chat_muted:
            if is_reaction || is_reply_to_own || is_webxdc_mention:
                if is_group:
                    if mentions_enabled:
                        DO_NOTIFY()
        else:
            DO_NOTIFY()

// in all other cases: do not notify
// in case the chat/app being notified is in scope, depending on UI, notification may be skipped

```
