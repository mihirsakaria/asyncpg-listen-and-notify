# PG Notify and listen
Run docker compose up

then create the trigger using the following sql commands in your postgresql database

```
create or replace function the_notification_trigger_function()
returns trigger language plpgsql as 
$$
begin
 perform pg_notify('<the_notification_channel>', to_json(new)::text);
 return null;
end;
$$;

create trigger the_notification_trigger
after insert on <table name> for each row
execute function the_notification_trigger_function()
```