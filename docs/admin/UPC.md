**Universal Product Code (UPC)**

This section explains how to implement and deploy UPC with Razuna.

**Enabling UPC**

The following criterion must be satisfied in order for UPC to be enabled:

 * UPC must be enabled for tenant under ‘Administration>Settings’

 * The folder with the UPC assets must have a label called ‘UPC’
 
 * User must be assigned to only one group with UPC size set. Assigning user to multiple UPC groups will result in an error message being shown to user while bulk downloading assets in the UI alerting him of the discrepancy.

 * With the above criterion met the UPC rules will take effect moving forward. Any existing assets will need to be re-uploaded for the rules to apply.

**File format and Uploading**

* The filename must contain the UPC number e.g. 123456789.1.tga
   
* The original file should have the .1 version embedded in the filename e.g. 123456780.1.tga, and must be the very first file uploaded before any renditions are uploaded.
    
* The renditions/views should have .2, .3 etc versions embedded in the filename e.g. 123456789.2.tga, 123456789.3.tga. Upon upload these will be associated as renditions to the original .1 file. The renditions are also renamed based on UPC naming conventions upon upload.

**Downloading**

* On download the folder structure in Razuna is maintained so if asset was in Folder1>Subfolder1>123456789.1.tga on download the same folder structure will be created for asset.
   
* Downloading assets has 2 options available which are set in the UPC group settings:

  * Download by creating UPC folder :

    * Each asset and its renditions is stored in its own folder which is created using UPC naming conventions (refer to [APPENDIX A](https://docs.google.com/document/d/10wydBlmAYSuktk61REuvvAAN-T90umBSzYlo1xh9abs/pub#id.a0wi2k922kre) )
    
    * So if asset was stored as Folder1>Subfolder1>Asset

    * On download the folder structure will be

    * Folder1>Subfolder1>56789>123456789.1.tga

  * Download without creating UPC folder

* UPC folder is not created for assets

**Searching**

 * To search for UPC numbers use the link titled ‘UPC Search’ next to the basic search
     
 * Partial UPC numbers are honored so searching for 3456 will return the 1234567890.1.tga asset
    
 * The search looks at the UPC fields and also the filenames

APPENDIX A 

___

**UPC NAMING CONVENTIONS**

The following functions are used to extract relevant UPC names for renditions and folders. All assets are stored in a 12 digit or more UPC format which includes the check digit. From this the client requested UPC format is extracted which may by 10, 11, 12 or more digits. Outputted formats of 10 & 11 do not include the check digit, but all others do.  

The Extract_UPC function takes the stored asset UPC string and based on the group UPC size set extracts the client requested format. The next function (Find_Manuf_String) takes the UPC string and returns the portion that is considered the manufacturer part, which is the Manuf-String. This string is used as the Folder Name of a length of 5 - 8 chars (numbers) which is used for creating the folder structure on download of assets if set for the UPC group. The final function (Find_Prod_String) takes same UPC string but returns the product side, which is the Prod_String of 5 - 6 chars(numbers). The Prod_String then has a file type extension appended to it, like .1 or .3 when outputting a Targa front view or Targa top view.  

Examples:

Client request 10 digit UPC, our file has 12 digits, say 122222333334, the extracted UPC would 2222233333, the folder created would be called 22222 and the front view targa image file would be    33333.1, side view 33333.2

Client request 12 digit UPC, our file has 12 digits, say 122222333334, the extracted UPC would 122222333334, the folder created would be called 1222223 and the front view targa image file would be    33334.1, side view 33334.2

Client request 11 digit UPC, our file has 13 digits, say 0122222333334, the extracted UPC would 12222233333, the folder created would be called 122222 and the front view targa image file would be    33333.1, side view 33333.2

Function Extract_UPC(sUPC As String, iUPC_Option As Integer) As String

'' Function Returns the requested size UPC from Root UPC based on UPC option selected

Dim sCheckDigit As String, sUPC_A As String

Dim alphaChar As Boolean

Dim iLen As Integer

Dim iLenA As Integer

On Error GoTo ErrorHandler

 '

 Extract_UPC = "NA"

 iLen = Len(sUPC)

 alphaChar = Right(sUPC, 1) Like ALPHA_CODE  'test rightmost postion for alpha

 If alphaChar = False Then

 ''   gb_strPkgeCode = " "

  Select Case iUPC_Option

   Case 10                ‘ 10 Digit size option

    Select Case iLen

       Case 14

           Extract_UPC = Mid(sUPC, 4, 10)

       Case 13

           Extract_UPC = Mid(sUPC, 3, 10)  

       Case 12

           Extract_UPC = Mid(sUPC, 2, 10)

       Case 11

           Extract_UPC = Mid(sUPC, 2, 10)

       Case Else

           Extract_UPC = sUPC

    End Select

   Case 11                ‘ 11 Digit size option

    Select Case iLen

       Case 14

           Extract_UPC = Mid(sUPC, 3, 11)

       Case 13

           Extract_UPC = Mid(sUPC, 2, 11)  

       Case 12

           Extract_UPC = Left(sUPC, 11)

       Case Else

           Extract_UPC = sUPC

    End Select

   Case 12                ‘ 12 Digit size option

    Select Case iLen

       Case 14

           Extract_UPC = Mid(sUPC, 3, 12)          

       Case 13

           Extract_UPC = Mid(sUPC, 2, 12)      

       Case Else

           Extract_UPC = sUPC

    End Select

   Case 13                        ‘ 13 Digit size option

    Select Case iLen

       Case 14

           Extract_UPC = Mid(sUPC, 2, 13)      

       Case Else

           Extract_UPC = sUPC

    End Select

   Case 14                ‘ 14 Digit size option

    Select Case iLen

       Case 14

           Extract_UPC = sUPC

       Case 13

           Extract_UPC = "0" & sUPC

       Case 12

           Extract_UPC = "00" & sUPC

       Case 11

           Extract_UPC = "000" & sUPC

       Case Else

           Extract_UPC = sUPC

    End Select

  End Select

 End If

Function Find_Manuf_String(ByVal strManuf_UPC As String) As String

    Dim RightMostChar As String

    Dim alphaChar  As Boolean

    Dim FldLen As Integer

   

    Find_Manuf_String = ""           ' set string to blank

    FldLen = Len(strManuf_UPC)      ' find out length of string

    alphaChar = Right(strManuf_UPC, 1) Like ALPHA_CODE  'test rightmost position for alpha

    If alphaChar = True Then

        If FldLen < 13 Then         ' if alpha and LT 13 postion, Manufacturer is 5 or 6 digits

            Find_Manuf_String = Left(strManuf_UPC, (FldLen - 6))

        Else

            Find_Manuf_String = Left(strManuf_UPC, (FldLen - 7))    ' else it is 7 digits

        End If

    Else

        If FldLen < 13 Then         ' if NOT alpha and LT 13 position, Manufacturer is 5 or 6 position

                            ' Sept08 corrected Apr08 fix change <12 to <13, so 12 digit 7/5 form

            If FldLen < 6 Then      ' FOR BAD DATA, LESS THEN 6 CHAR

                    Find_Manuf_String = "00000"        ' set manuf to "00000"

            Else

                                Find_Manuf_String = Left(strManuf_UPC, (FldLen - 5))

            End If

        Else                ' Apr 2008  14 digit UPC  8/6  output form

            Find_Manuf_String = Left(strManuf_UPC, (FldLen - 6))  

        End If

    End If  

End Function

Function Find_Prod_String(ByVal strManuf_UPC As String) As String

    Dim RightMostChar As String

    Dim alphaChar  As Boolean

    Dim FldLen As Integer

   

    Find_Prod_String = ""           ' set string to blank

    FldLen = Len(strManuf_UPC)      ' find out length of string

    alphaChar = Right(strManuf_UPC, 1) Like ALPHA_CODE  'test rightmost position for alpha

    If alphaChar = True Then

        If FldLen < 14 Then         ' if alpha and LT 14 position, PrdUPC is 6 position

            Find_Prod_String = Right(strManuf_UPC, 6)

        Else

            Find_Prod_String = Right(strManuf_UPC, 7)    ' else it is 7 positions

        End If

    Else

        If FldLen < 13 Then         ' if NOT alpha and LT 14 position, PrdUPC is 5 position

            Find_Prod_String = Right(strManuf_UPC, 5)

        Else

            Find_Prod_String = Right(strManuf_UPC, 6)     ' else it is 6 positions

        End If

    End If    

End Function


