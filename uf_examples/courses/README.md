# Add courses to UF VIVO

UF makes a clear distinction between a course (abstract) and a course section (instance).  A course has a uf
extension common course number which serves as a key.

This requires an extension to the VIVO course model.  vivo:Course is a class that corresponds to the course section 
described above.  ufc:Course is a new class that corresponds to the more abstract entity.

## Attributes

1. Common course number
1. Course Title (VIVO Label)
1. Type is ufc:Course

## Process

Courses (ufc:course) are added before course sections (vivo:Course).  Course sections relate people to courses as 
instructors.

## Filters

1. Manage_columns_filter -- remove all but the ccn and label.  Add an empty uri and remove column.
Everything else relates to course sections.
1. unique_ccn_filter -- remove duplicate ccn.
1. merge_filter -- look every course up in VIVO by ccn.  Assign uri

    cat course_data.csv | python manage_columns_filter.py | python unique_ccn_filter.py | 
    python merge_filter.py > course_update_data.txt