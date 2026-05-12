
# Props --- 

1st way -- <Component inputs={`{inputs.step${currentStep}}`} /> 

2nd way -- <Component {...inputs[`step${currentStep}`]} onChange={handleChange} /> 

-- accessing like this
{firstName, lastName, onChange = () }

* 2 destructuring happening at same time ->  props - {} then firstName, lastName are directly accessed from props, that won't work. If we want this to work, we have to do it like 2nd way -> 
