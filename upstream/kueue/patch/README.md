# Patches

## e2e.patch

This patch sets up our e2e tests to skip waiting for operators as the namespace name is different and set up our namespaces. It also skips the configuration change for admission fair sharing as the configuration is managed in the Kueue instance.

## test_util_e2e.patch

This patch modifies `test/util/e2e.go` to add the `kueue.openshift.io/managed` label to namespaces created in e2e tests and increases the metrics timeout from `LongTimeout` to `VeryLongTimeout`.

## e2e_timeout_ocp.patch

This patch increases test timeout values for the upstream e2e tests that wait for pod/replica readiness and workload completion. On OpenShift (especially HyperShift), pod scheduling, image pulling, and container startup take significantly longer than on kind clusters, causing tests to time out at `MediumTimeout` (45s). This patch bumps:
- `MediumTimeout` → `LongTimeout` (45s → 90s) in `statefulset_test.go`, `deployment_test.go`, and `visibility_test.go`
- `LongTimeout` → `VeryLongTimeout` (90s → 5min) in `e2e_v1beta1_test.go`

## golang-1.24.patch

This patch can be dropped once there is a golang 1.25 builder image.
