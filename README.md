select  pc.display_name, 
  case when sc.display_name is null then 'No Employer' else sc.display_name end Employer,
  count(ccc.case_id) NuberOfCases
from civicrm_contact pc
left join civicrm_contact sc on sc.id=pc.employer_id
left join civicrm_case_contact ccc on ccc.contact_id=pc.id
left join civicrm_case cc on cc.id = ccc.case_id
where pc.contact_type = 'Individual'
group by pc.display_name, sc.display_name 
order by pc.display_name 
