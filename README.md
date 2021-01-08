public class AccountsByIndustry 
{

    //Return account records and message to be displayed in toast
    @AuraEnabled
    public static List<Account> getAccounts()
    {
        List<Account> lstAccountResults = new List<Account>();
       
            lstAccountResults = [select Id,Name,Owner.Name,Phone,Website,AnnualRevenue,Industry from Account
                                           where Industry ='Financial Services'
                                           ORDER BY Name 
                                           DESC NULLS LAST];
            
        
        return lstAccountResults;
    }
    
    @AuraEnabled
    public static Boolean checkingAccountAccess(String strAccRecId)
    {
        Boolean blnResult = false;
        UserRecordAccess getRecordAccess = [SELECT RecordId,HasEditAccess,HasReadAccess FROM UserRecordAccess 
                                      WHERE UserId=: UserInfo.getUserId() AND RecordId=:strAccRecId];
        if(getRecordAccess.HasEditAccess)
            blnResult = true;
        
        return blnResult;
        
    }
    
}
