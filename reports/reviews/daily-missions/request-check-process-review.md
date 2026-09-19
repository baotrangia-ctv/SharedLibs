# Request–Check–Process review — Daily Missions

Status: **Pass**.

Mission claim, claim-all, and milestone claim each expose a Request method that initializes outputs, calls a Check method, returns a stable status on failure, and mutates state only through Process after a successful check. The `canDeliverRewards` preflight prevents the shared core from marking a claim before the consumer confirms delivery capability.

