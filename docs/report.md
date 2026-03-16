# NonDex Flaky Test Reproduction

## CI Workflow
The GitHub Actions workflow runs the target test both normally and using the NonDex Maven plugin.

Workflow file:
.github/workflows/nondex.yml

## CI Run
https://github.com/shloka-22/jackrabbit-oak/actions/runs/23122265640

## Observed Behavior

Normal test execution:
PASS

NonDex execution:
FAIL

The following test fails under NonDex across multiple seeds:

org.apache.jackrabbit.oak.security.authentication.ldap.GuestTokenDefaultLdapLoginModuleTest#testLoginSetsAuthInfo

## Explanation

The test passes when executed normally but fails when NonDex randomizes the order of operations.  
This indicates the test depends on nondeterministic behavior such as iteration order.
Consequently, the test is flaky.
