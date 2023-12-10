# Protection
> [!tldr] Isolate buggy programs, bad people, and user errors

## Pre-emption
* Ability to give and take away resources
* Have periodic timer [[Interrupts]]
	* If a process used up quantum (small amount of time allowed to run) → schedule another

## Interposition or Mediation
 * OS is between application and resources
 * Track all resources available for an application
	* E.g. in table
 * For each access attempt, ==check if it is legal in the table==

## Privileged and Unprivileged modes
* User applications have ==unprivileged access/user mode==
* OS has ==privileged access/kernel mode==
