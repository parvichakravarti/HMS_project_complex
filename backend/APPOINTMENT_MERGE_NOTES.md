# Appointment backend update

## Changes in this package

- Updated the legacy reference appointment entity to reference the existing `Patient` JPA entity instead of the duplicate `PatientRecord` entity.
- Updated `ReferenceService` to use `Patient` consistently and convert the patient's UUID to the string expected by the legacy response DTO.
- Removed duplicate `Patient` / `PatientRecord` imports from `ReferenceService`.

## Important scope note

This is a compatibility/compile-fix update for the legacy reference appointment path. It does **not** yet consolidate `/api/appointments` into the modern `/api/v1/appointments` service. The legacy controller and DTO contract are retained because the Flutter offline-sync DAO still calls `/api/appointments`.

The legacy `AppointmentRecord` still maps legacy columns (`appointment_date`, `time_slot`, `token_no`, `visit_type`, `doctor_id`) while migration V8 defines the modern appointments schema (`starts_at`, `ends_at`, `doctor_uuid`, etc.). Do not treat this package as proof that the legacy appointment endpoints are database-compatible with a database created only from the current migrations.

## Validation

The Maven wrapper could not run in this environment because it attempted to download Maven 3.10.0 and network access to Maven Central was unavailable. Run `mvnw.cmd -DskipTests compile` on the development machine, then run backend tests and exercise both appointment API paths against the configured database.
