Formal Verification of Role-Based Access Control in Enterprise Systems

Project proposal for the Software Verification course. Dear Professor, we would like to propose the project described in this repository for the Software Verification course. We would appreciate your feedback on the topic and its suitability for the course.

	
Team	TAG
Members	Swapnil Jadhavar, Ruchika Bhamre
Verification tool	Dafny (with the Z3 SMT solver)
Status	Proposal stage: no code yet, the layout in section 5 is planned
1. Problem statement

Enterprise systems give people access to sensitive resources such as files, records and services. Incorrect permission handling or role management can result in unauthorized access and security vulnerabilities.

2. Motivation

Traditional testing cannot exhaustively cover every combination of users, roles, permissions and state changes. We want to use formal verification to establish machine-checked correctness guarantees for a role-based authorization system, guarantees that hold for all states, not just the ones we thought to test.

3. Proposed work
Design and implement a general role-based access control (RBAC) model.
Specify the authorization rules in Dafny.
Formally verify:
P1 Unauthorized-access prevention (default deny; access only via a role that grants it)
P2 Role revocation correctness (a revoked role no longer grants access, and revocation never escalates privileges)
P3 Separation of duties (no user ever holds two conflicting roles)
P4 Invariant preservation (every operation keeps the system in a valid state)
Demonstrate verification of valid implementations and of deliberately faulty ones (the faulty ones must be rejected by the verifier).
Evaluate the approach and document its limitations.
4. Expected outcome

A small, formally verified RBAC prototype, including:

machine-checked proofs (Dafny),
an illustrative application,
tests,
technical documentation.
5. How Dafny is used

Dafny is a programming language with a built-in verifier. Code and specification are written together; Dafny turns them into proof obligations and the Z3 SMT solver checks them at compile time.

Dafny feature	Use in this project
Datatypes	The system state: user-to-roles map, role-to-permissions map, conflict set
Predicates	The access decision (CanAccess) and the validity invariant (Valid)
requires / ensures	Contracts on every operation (assign role, revoke role, grant permission)
Lemmas	Properties that span operations, e.g. revocation never escalates privileges
Verifier errors	Evidence that the faulty implementations are rejected
dafny run / dafny test	The demo application and the runtime tests
6. Model at a glance
Resources: anything that needs protection, identified by name (e.g. file:payroll, service:billing).
Permission: an action (Read, Write, Execute, Approve) on a resource.
Roles grant sets of permissions; users hold sets of roles.
Conflicts are pairs of roles that no single user may hold together (separation of duties), e.g. Requester and Approver: whoever submits a request must not approve it.
Access decision: allow iff one of the user's roles grants the permission; deny otherwise.

Readme
MD
Web search
Memory
Read · Software Verification Project
