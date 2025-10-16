
# Documentazione Web Services — local_wsvecomp

Questa documentazione copre gli endpoint RESTful esposti dal plugin.

## Indice
- [Autenticazione](./auth.md)
- [Convenzioni](./conventions.md)
- [Gestione errori](./errors.md)
- Endpoints:
  - [core_user_create_users](./endpoints/core_user_create_users.md)
  - [core_user_delete_users](./endpoints/core_user_delete_users.md)
  - [core_user_update_users](./endpoints/core_user_update_users.md)
  
  - [core_course_create_courses](./endpoints/core_course_create_courses.md)
  - [create_courses_with_sections](./endpoints/create_courses_with_sections.md)
  - [core_course_delete_categories](./endpoints/core_course_delete_categories.md)
  - [core_course_delete_courses](./endpoints/core_course_delete_courses.md)
  - [core_course_delete_modules](./endpoints/core_course_delete_modules.md)
  - [core_course_duplicate_course](./endpoints/core_course_duplicate_course.md)
  - [core_course_get_categories](./endpoints/core_course_get_categories.md)
  - [core_course_get_contents](./endpoints/core_course_get_contents.md)
  - [core_course_get_courses](./endpoints/core_course_get_courses.md)
  - [core_courseformat_new_module](./endpoints/core_courseformat_new_module.md)
  - [core_course_get_courses_by_field](./endpoints/core_course_get_courses_by_field.md)
  - [core_course_get_course_module](./endpoints/core_course_get_course_module.md)
  - [core_course_search_courses](./endpoints/core_course_search_courses.md)
  - [core_course_update_categories](./endpoints/core_course_update_categories.md)
  - [core_course_update_courses](./endpoints/core_course_update_courses.md)
  - [local_wsvecomp_move_activity_between_courses](./endpoints/move_activity_between_courses.md)
  - [local_wsvecomp_move_activity_within_section](./endpoints/move_activity_within_section.md)
  - [local_wsvecomp_reorder_activity_within_section](./endpoints/reorder_activity_within_section.md)
  - [local_wsvecomp_add_vimeoactivity_to_course](./endpoints/add_vimeoactivity_to_course.md)
  - [local_wsvecomp_delete_activity_from_course](./endpoints/delete_activity_from_course.md)
  - [local_wsvecomp_program_create](./endpoints/program_create.md)
  - [local_wsvecomp_program_update](./endpoints/program_update.md)
  - [local_wsvecomp_program_get](./endpoints/program_get.md)
  - [local_wsvecomp_program_list](./endpoints/program_list.md)
  - [local_wsvecomp_program_set_structure](./endpoints/program_set_structure.md)
  - [local_wsvecomp_program_set_structure_tree](./endpoints/program_set_structure_tree.md)
  - [enrol_programs_source_manual_allocate_users](./endpoints/source_manual_allocate_users.md)
  - [local_wsvecomp_get_user_progress](./endpoints/get_user_progress.md)
  - [local_wsvecomp_trigger_welcome](./endpoints/trigger_welcome.md)


## Quick start
- Base: `/webservice/restful/server.php`
- Auth: `Authorization: Bearer <TOKEN>`
- JSON in input/output
- Ultimo update: 2025-09-19
