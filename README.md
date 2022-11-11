# Sprint-Education-Mission

public class SprintEducation {
    

    public static void EnrolmentProgressionStatus(){
        List<Contact> educList = [SELECT Id, Prior_Qualification__c, Enrolment_Progression__c FROM Contact];        
        List<Contact> educToUpdate = new list<Contact>();

        for(Contact con:educList){
            if(con.Prior_Qualification__c == 'Below Tertiary'){
                con.Enrolment_Progression__C = 'Advanced';
                educToUpdate.add(con);    
            }
            if(con.Prior_Qualification__c == 'Tertiary Graduate'){
                con.Enrolment_Progression__c = 'Ultimate';
                educToUpdate.add(con);       
            }
            if(con.Prior_Qualification__c == 'Tertiary Post-Graduate'){
                con.Enrolment_Progression__c = 'Extra';
                educToUpdate.add(con);       
            }
        }
          update educToUpdate;
          system.debug(educToUpdate);       	
    }//End of Loop
}// End of class


Test 

apex trigger when creating a new student record enrolment is created for sprint training.

trigger Apex9Trigger on Contact (before insert,before update,after insert, after update) {
    
    for(Contact c:Trigger.new){
        
        
        if(Trigger.isAfter){
            if(Trigger.isInsert){
                
                             
                
                Enrollment__c newcourse= new Enrollment__c();
                newcourse.Sprint_Education__c ='a005h00000f9tzmAAA';
                newcourse.Student__c =c.Id;
                
                insert newcourse;
                
                
                
                
            }
        }
        
        
        
    }
    
    

}


Test

@istest
private class testApex9Trigger {
    
    @isTest
    private static void testtrigger(){
        
        Contact c = new Contact();
        c.FirstName ='Nupur';
        c.LastName = 'Kapor';
        c.Prior_Qualification__c = 'Tertiary Graduate';
        c.Enrolment_Progression__c = 'Extra';
        
        insert c;
        
      List<Enrollment__c> cList=[SELECT Id,Student__c,Sprint_Education__c FROM Enrollment__c where Student__c=:c.Id];
        
        system.assertEquals('a005h00000f9tzmAAA', cList[0].Sprint_Education__c);
            
        
        
        
        
        
    }
    
    
    
    
    
    

}












