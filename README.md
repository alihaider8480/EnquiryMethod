package com.temenos.t24.api.hook.system
/**
*The EnquiryHook component allows access to routines for customising ENQUIRY.<br>
* There are hooks for BUILD.ROUTINE, CONVERSION and for NOFILE enquiries.
*/
public class Enquiry {
    /**
    * This interface enables the implementer to set the selection criteria used by the enquiry engine to select records.<br>
    * This interface is invoked after the user has entered their choices in the selection screen, so the implementor has the opportunity to override user choices.
    * This interface provides access to the parameter usually named 'ENQ.DATA' in the enquiry build routine.
    * Note that the FIXED.SELECTION defined for the enquiry is executed before this interface, the filter criteria returned by this routine will
    * operate on the subset of records returned by the FIXED.SELECTION. This is standard T24 enquiry build routine behaviour.<br>
    * <br/><b>T24 Details:</b>The EB.API hook used by this interface is ENQUIRY.BUILD.ROUTINE.HOOK.
    * The T24 field specifying this hook is the BUILD.ROUTINE field in ENQUIRY.<br>
    * If an exception is thrown in the implementing class, the exception message will be displayed on screen and no enquiry results will be displayed.
    * <br>
    * @param filterCriteria List<com.temenos.t24.api.complex.eb.enquiryhook.FilterCriteria> : The list of FilterCriteria as entered by the user. (In T24 terms, this is ENQ.DATA<2 ... 4>)<br>
    * @param enquiryContext com.temenos.t24.api.complex.eb.enquiryhook.EnquiryContext : Context variables for the enquiry interaction.<br>
    * @return List<com.temenos.t24.api.complex.eb.enquiryhook.FilterCriteria> : A new list of filter criteria to be applied during record selection.<br>
    */
    public List<com.temenos.t24.api.complex.eb.enquiryhook.FilterCriteria> setFilterCriteria(List<com.temenos.t24.api.complex.eb.enquiryhook.FilterCriteria> filterCriteria, com.temenos.t24.api.complex.eb.enquiryhook.EnquiryContext enquiryContext){}

    /**
    * This interface enables the implementer to set the selection criteria using the values of the current record from an input screen.<br>
    * This interface is invoked when the user activates a dropdown list to get the available values for the field to which the dropdown enquiry is attached.
    * <br/><b>T24 Details:</b> The EB.API hook used by this interface is ENQUIRY.BUILD.ROUTINE.HOOK.<br/>
    * The T24 field specifying this hook is the BUILD.ROUTINE field in ENQUIRY.<br/>
    * A dropdown enquiry is associated with a field through the VERSION->DROP.DOWN field and allows the selection criteria to be defined based on the current value of fields in the screen.<br/>
    * This interface provides access to the parameter usually named 'ENQ.DATA' in the enquiry build routine.
    * Note that the FIXED.SELECTION defined for the enquiry is executed before this interface, the filter criteria returned by this routine will
    * operate on the subset of records returned by the FIXED.SELECTION. This is standard T24 enquiry build routine behaviour.<br/>
    * If an exception is thrown in the implementing class, the exception message will be displayed on screen and no enquiry results will be displayed.
    * <br>
    * @param filterCriteria List<com.temenos.t24.api.complex.eb.enquiryhook.FilterCriteria> : The list of FilterCriteria as entered by the user. (In T24 terms, this is ENQ.DATA<2 ... 4>)<br>
    * @param currentRecord TStructure : The current record to which the dropdown enquiry is attached. (In T24 terms, this is R.NEW)<br>
    * @param enquiryContext com.temenos.t24.api.complex.eb.enquiryhook.EnquiryContext : Context variables for the enquiry interaction.<br>
    * @return List<com.temenos.t24.api.complex.eb.enquiryhook.FilterCriteria> : A new list of filter criteria to be applied during record selection.<br>
    */
    public List<com.temenos.t24.api.complex.eb.enquiryhook.FilterCriteria> setDropdownFilterCriteria(List<com.temenos.t24.api.complex.eb.enquiryhook.FilterCriteria> filterCriteria, TStructure currentRecord, com.temenos.t24.api.complex.eb.enquiryhook.EnquiryContext enquiryContext){}

    /**
    * This interface enables the implementer to set the value of an element displayed in the enquiry results programatically to a list of values.<br>
    * This interface is invoked during calculation of each field's value, in the order it is specified in the list of CONVERSION fields in the enquiry definition.
    * The current value of the field will be passed in, and can be used as input for any kind of conversion that is not supported by the inbuilt conversion types.
    * This interface is similar to setValue() but should be used to return a list of values instead of a single value.
    * The value returned by this interface is written to O.DATA. Items in the list are converted to separate multivalues.<br>
    * Note: this interface will be called once for each item in the returned list. If generating the list is expensive then consider caching it and reusing it.<br>
    * <br/><b>T24 Details:</b> The EB.API hook used by this interface is ENQUIRY.CONVERSION.HOOK.
    * The T24 field specifying this hook is the CONVERSION field in ENQUIRY.<br>
    * If an exception is thrown in the implementing class, the exception message will be displayed on screen and no enquiry results will be displayed.
    * <br>
    * @param value String : The initial value of the field. The new value should be returned. (In T24 terms, this is O.DATA)<br>
    * @param currentId String : The ID of the current record being processed. (In T24 terms, this is the 'ID' common variable)<br>
    * @param currentRecord TStructure : The full record currently being processed by the enquiry. (In T24 terms, this is R.RECORD)<br>
    * @param filterCriteria List<com.temenos.t24.api.complex.eb.enquiryhook.FilterCriteria> : The list of selection criteria entered by the user. (In T24 terms, this is fields<2 ... 4> from ENQ.SELECTION)<br>
    * @param enquiryContext com.temenos.t24.api.complex.eb.enquiryhook.EnquiryContext : Context variables for the enquiry interaction.<br>
    * @return List<String> : The new value to be displayed to the enquiry processing engine, to be displayed to the user or used in further calculations.<br>
    */
    public List<String> setValues(String value, String currentId, TStructure currentRecord, List<com.temenos.t24.api.complex.eb.enquiryhook.FilterCriteria> filterCriteria, com.temenos.t24.api.complex.eb.enquiryhook.EnquiryContext enquiryContext){}

    /**
    * This interface enables the implementer to set the entire contents of a record prior to it being processed by the enquiry engine.<br>
    * This interface is invoked during enquiry processing when the field it is attached to is calculated.<br>
    * <br/><b>T24 Details:</b> The EB.API hook used by this interface is ENQUIRY.CONVERSION.HOOK.
    * The T24 field specifying this hook is the CONVERSION field in ENQUIRY.<br>
    * This interface is mainly intended to support NOFILE enquiry in T24. One strategy for building NOFILE enquiries uses a CONVERSION routine to
    * modify the virtual 'record' being processed at runtime. This interface supports that strategy.
    * The output of this routine is written to the 'record' currently being used by the enquiry.
    * The structure of the record is defined in the STANDARD.SELECTION definition for the NOFILE, by the 'D' type fields.
    * The NOFILE application should be introspected to generate .domain objects for it, this will then create 'Record' objects for the nofile application.<br>
    * The setRecord() and setValue() interfaces are both triggered from the CONVERSION field but differ in purpose and effect.
    * The currentRecord parameter of this method is used to overwrite R.RECORD for the current record being processed.<br>
    * If an exception is thrown in the implementing class, then the exception message will be displayed on screen and no enquiry results will be displayed.<br>
    * @param value String : The initial value of the field to which the interface is attached. (In T24 terms, this is O.DATA)<br>
    * @param currentId String : The ID of the current record being processed. (In T24 terms, this is the 'ID' common variable)<br>
    * @param currentRecord TStructure : The full record currently being processed by the enquiry. (In T24 terms, this is R.RECORD)<br>
    * @param filterCriteria List<com.temenos.t24.api.complex.eb.enquiryhook.FilterCriteria> : The list of selection criteria entered by the user. (In T24 terms, this is fields<2 ... 4> from ENQ.SELECTION)<br>
    * @param enquiryContext com.temenos.t24.api.complex.eb.enquiryhook.EnquiryContext : Context variables for the enquiry interaction.<br>
    */
    public void setRecord(String value, String currentId, TStructure currentRecord, List<com.temenos.t24.api.complex.eb.enquiryhook.FilterCriteria> filterCriteria, com.temenos.t24.api.complex.eb.enquiryhook.EnquiryContext enquiryContext){}

    /**
    * This interface enables the implementer to define the list of record Ids that the enquiry will process.<br>
    * This interface is invoked during the record selection stage of running an enquiry, and replaces the usual record selection based on a select statement on a T24 application.
    * <br/><b>T24 Details:</b> The EB.API hook used by this interface is SS.SYS.FIELD.NO.HOOK.
    * The T24 field specifying this hook is the SYS.FIELD.NO in STANDARD.SELECTION (the SYS.TYPE must be 'R' in the associated multivalue group)<br>
    * This interface is mainly intended to support NOFILE enquiry in T24. It supports the 'R' type routine specified in STANDARD.SELECTION for the nofile table.
    * The implementer is expected to generate a list of recordIds for use in the enquiry processing.<br>
    * Note: Some nofile enquiries exploit a trick of returning all required information inside the recordId, delimited with some value, for example '*', and then
    * extract the values from the recordId using the F(IELD) conversion in the enquiry.<br>

    * If an exception is thrown in the implementing class, then the exception message will be displayed on screen and no enquiry results will be displayed.
    * <br>
    * @param filterCriteria List<com.temenos.t24.api.complex.eb.enquiryhook.FilterCriteria> : The list of selection criteria entered by the user. In T24 terms, this comes from the common variables D.FIELDS, D.RANGE.AND.VALUE and D.LOGICAL.OPERANDS.<br>
    * @param enquiryContext com.temenos.t24.api.complex.eb.enquiryhook.EnquiryContext : Context variables for the enquiry interaction.<br>
    * @return List<String> : The list of recordIds.<br>
    */  

    is interface ma hum list of records id ko laka process karta hai
    or ya call hoti hai selection stage enquiry pa or replace karti hai mamuli selection based record ko select statement ki t4 application sa
    or is ka lia hum ss bnata hai or us ma sys.type R multi value group ka lia
    or ya method ko hum nofile enquiry ka lia use karta hai or ss ma hum is routine ki type R rakhta hai phechana ka lia ka ya no file hai
    or ya list of records ids ko use karta hai enquiry ma
    ya nofile enquiry ya bhi karti hai ka tamam records ids jo wo return kar raha hai us recordsids ka anadar ka data bhi return karti hai "*" laga ka
    matlab ids bhi return karti hia or uska aik aik ids ka data bhi matlab extract karti hai records from recordids using F(IELD) conversion
    agar exception ati hai class ma to error bhi dagi screen pa or koi result display ni hoga

    (2 parameter lati hai)
    1: filterCriteria is ka andar list hogi jo user na filterCriteria ma di hogi single record bhi da sakta hai or ya in variables ma ajae ga data 
       (D.FIELDS, D.RANGE.AND.VALUE and D.LOGICAL.OPERANDS ) jo user na dia hoga.
    2: enquiryContext is ma context variable hota hai enquiry ka
    
    public List<String> setIds(List<com.temenos.t24.api.complex.eb.enquiryhook.FilterCriteria> filterCriteria, com.temenos.t24.api.complex.eb.enquiryhook.EnquiryContext enquiryContext){}

    /**
    * This interface enables the implementer to set the value of an element displayed in the enquiry results programatically.<br>
    * This interface is invoked during calculation of each field's value, in the order it is specified in the list of CONVERSION fields in the enquiry definition.
    * The current value of the field will be passed in, and can be used as input for any kind of conversion that is not supported by the inbuilt conversion types.
    * The value returned by this interface is written to O.DATA.<br>
    * <br/><b>T24 Details:</b> The EB.API hook used by this interface is ENQUIRY.CONVERSION.HOOK.
    * The T24 field specifying this hook is the CONVERSION field in ENQUIRY.<br>
    * If an exception is thrown in the implementing class, the exception message will be displayed on screen and no enquiry results will be displayed.
    * <br>
    * @param value String : The initial value of the field. The new value should be returned. (In T24 terms, this is O.DATA)<br>
    * @param currentId String : The ID of the current record being processed. (In T24 terms, this is the 'ID' common variable)<br>
    * @param currentRecord TStructure : The full record currently being processed by the enquiry. (In T24 terms, this is R.RECORD)<br>
    * @param filterCriteria List<com.temenos.t24.api.complex.eb.enquiryhook.FilterCriteria> : The list of selection criteria entered by the user. (In T24 terms, this is fields<2 ... 4> from ENQ.SELECTION)<br>
    * @param enquiryContext com.temenos.t24.api.complex.eb.enquiryhook.EnquiryContext : Context variables for the enquiry interaction.<br>
    * @return String : The new value to be displayed to the enquiry processing engine, to be displayed to the user or used in further calculations.<br>
    */
    public String setValue(String value, String currentId, TStructure currentRecord, List<com.temenos.t24.api.complex.eb.enquiryhook.FilterCriteria> filterCriteria, com.temenos.t24.api.complex.eb.enquiryhook.EnquiryContext enquiryContext){}

}
