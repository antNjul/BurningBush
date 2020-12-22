<?xml version="1.0"?>

-<list>


-<com.ncr.payments.configuration.ConfigurationItem>

<instanceId>38</instanceId>

<createDate>2018-10-31T19:20:09.165</createDate>

<lastModifyDate>2018-10-31T19:20:09.165</lastModifyDate>

<description> User Should log out and re-login after publishing changed contents in CommonComponent configuration</description>

<environment>install</environment>

<name>CommonComponent</name>

<setId>0</setId>

<module>CommonComponent</module>


-<value>

-<![CDATA[<node name='Common'>
			<entry key='ghostDocumentsImageFile.root'	value='c:/' />
			<entry key='orgId'	value='1' />
			<entry key='applicationName'	value='TC' />
		</node>
		<node name='CommonComponent'>
		
		<!-- In below example, <groupname> in configuration file should be replaced with the group name needs to to be ignored to display on End Item Collection screen.-->
		
		<!-- ##########################################################################################################################-->
				<!--
					The configuration file contains the key and value pairs.
					The maximum characters allowed in key is 80 characters.
					The maximum characters allowed in value is 8192.
				-->
				<!-- ################################################# End of Comments ########################################################-->
				
		<node name='ExcludeItemCollectionGroup'> 
			<map> 
			<!-- 
			    <entry key='<groupname>' value='Commercial'/> 
				<entry key='<groupname>' value='Commercial'/> 
				For ex: <entry key='rdbEas' value='Commercial'/> 
				<entry key='<groupname>' value='ATM'/> 				
			-->
			</map> 
		 </node>
		
				<!-- DRN Configuration - START-->
				<!--This drn formatting configuration will be used when the generateDrnDefault is set to false and the generateDrn is either set to false or not set for a particular group.-->
				<node name='drnConfig'>
					<!-- # DRN format is "ttrrttyyyymmddssss" # - rr is 2 digit region code 
						# - yyyymmdd is for the cycle date # - tttt is 4 digit station number # - 
						ssss is 4 digit sequence number -->
					<entry key='drn'
						value='{stationNumber,xstring,%r0r2sl}{regionCode,xstring,%l0l2sl}{str1}{str2}' />
					<node name='drn-parts'>
						<entry key='str1'
							value='{stationNumber,xstring,%l0l2sl}{cycleDate,date,yyyyMMdd}' />
						<entry key='str2' value='{nextDrnSequenceNumber,number,0000}' />
					</node>
				</node>
				
				<!-- This drn formatting configuration will be used when the generateDrnDefault is set to false and the generateDrn is set to true for a particular group.-->
				<node name='tcDrnConfig'>
					<!-- # DRN format is "ttrrttyyyymmddssss" # - rr is 2 digit region code 
						# - yyyymmdd is for the cycle date # - tttt is 4 digit station number # - 
						ssss is 4 digit sequence number -->
					<entry key='drn'
						value='{stationNumber,xstring,%r0r2sl}{regionCode,xstring,%l0l2sl}{str1}{str2}' />
					<node name='drn-parts'>
						<entry key='str1'
							value='{stationNumber,xstring,%l0l2sl}{cycleDate,date,yyyyMMdd}' />
						<entry key='str2' value='{nextDrnSequenceNumber,number,0000}' />
					</node>
				</node>
				<!--This config node will be used to format drn (for all the groups) when the generateDrnDefault is set to true.-->
				<!--Only If the generateDrnDefault is set to false,then this drnformat config will be used only for those groupswhose generatedrn is set to true.-->
				<node name='tcDrnFormat'>
					<!-- # DRN format is "ttrrttyyyymmddssss" # - rr is 2 digit region code 
						# - yyyymmdd is for the cycle date # - tttt is 4 digit station number # - 
						ssss is 4 digit sequence number -->
					<entry key='drn'
						value='{stationNumber,xstring,%r0r2sl}{regionCode,xstring,%l0l2sl}{str1}{str2}' />
					<node name='drn-parts'>
						<entry key='str1' value='00' />
						<entry key='str2' value='{nextDrnSequenceNumber,number,000000}' />
					</node>
				</node>
								
				
				<!-- DRN Configuration - END -->
				
					
				<map>
	                <!-- <entry key='defaultCutOverTime' value='23:59:59' /> -->
					<!-- Specify the image data file size in Bytes , 5120 is 5KB -->
					<entry key='cutoffByGroup' value='false' />
					
					<entry key='defaultBatchMaxItemCount' value='3000' /> <!-- number of items -->
					<entry key='defaultBatchMaxValue' value='9999999999999999' />
					<entry key='holdoverDateSwitchTimeSchedule' value='default' />
					<entry key='defaultRegionCode' value='Region1' />
					<!-- Below parameter for DRN -->
					<entry key='regionCode' value='66' />
					<entry key='generateDrnDefault' value='true' />
					<entry key='GENERATOR_NAME' value='TcSequence' />
					<entry key='fieldOrderFormat' value='CPCS' />
						<!-- Below parameter SCER-2429-->
					<entry key='enableGroupExport' value='true' />
					<entry key='itemIdGeneratorName' value='WBIitemIdGenerator' />
					<entry key='depositIdGeneratorName' value='WBIdepositIdGenerator' />
					<entry key='depositIdCacheLimit' value='500' />
					<entry key='Autobalancing' value='false' /> 
					<entry key='enableGroupChannelMapping' value='true' /> 
					<!-- Consider holidays for HoldOver -->
					<entry key='TGHoldOverIncludeHoliday' value='false' />
					
				</map>
					
					
				<!-- Sequence Configuration AT Common Component Level - START -->
				<node name='sequences'>
					<!-- <node name='TransactionSubSequence'></node>
					<node name='BatchHeaderSubSequence'></node>
					<node name='BatchTrailerSubSequence'></node>
					<node name='ItemCollectionHeaderSubSequence'></node>
					<node name='ItemCollectionTrailerSubSequence'></node> -->

					<node name='ItemDrnSequence'>
						<map>
							<entry key='initialValue' value='1' />
							<entry key='maximumValue' value='9223372036854775806' />
							<entry key='incrementStep' value='1' />
							<entry key='rollOver' value='true' />
							<entry key='hardReset' value='9223372036854775807' />
							<entry key='resetTo' value='1' />
							<entry key='resetDRNDaily' value='true' />
							<entry key='numberOfValues' value='500' />
						</map>
					</node>
				</node>

				
				<node name='groupDefinition'>
					<node name='sourceTypes'>
						<node name='ATM'>
							<entry key='BranchNumber' value='9999' />
						<entry key='priority' value='1' /><!--Priority in eips output file Name -->
							<map>
								<entry key='configKey' value='SourceId' />
								<entry key='holdoverDateSwitchTimeSchedule' value='default' />
							</map>
							<node name='groupMapping'>
								<map>
									<!-- KEY names are configKey pattern values and these values can 
										also have wildcards, where '*' is for none or any string and '?' is for single 
										character -->
								<entry key='IOR*' value='PT'/>
								<entry key='IAZ*' value='PT'/>
								<entry key='ICO*' value='MT'/>
								<entry key='INV*' value='PT'/>
								<entry key='IWA*' value='PT'/>
								<entry key='IID*' value='MT'/>
								<entry key='INM*' value='MT'/>
								<entry key='ITX*' value='MT'/>
								<entry key='IOK*' value='CT'/>
								<entry key='IAR*' value='CT'/>
								<entry key='IIA*' value='CT'/>
								<entry key='IKS*' value='CT'/>
								<entry key='IIL*' value='CT'/>
								<entry key='IMO*' value='CT'/>
								<entry key='IMN*' value='CT'/>
								<entry key='ITN*' value='CT'/>
								<entry key='IKY*' value='CT'/>
								<entry key='IKY*' value='CT'/>
								<entry key='IGA*' value='ET'/>
								<entry key='ISC*' value='ET'/>
								<entry key='INC*' value='ET'/>
								<entry key='IVA*' value='ET'/>
								<entry key='IDC*' value='ET'/>
								<entry key='IMD*' value='ET'/>
								<entry key='IOH*' value='ET'/>
								<entry key='ITN*' value='ET'/>
								<entry key='INJ*' value='ET'/>
								<entry key='IPA*' value='ET'/>
								<entry key='INY*' value='ET'/>
								<entry key='IRI*' value='ET'/>
								<entry key='INH*' value='ET'/>
								<entry key='IME*' value='ET'/>
								<entry key='ICT*' value='ET'/>
								<entry key='ICA*' value='PT'/>
								<entry key='IFL*' value='ET'/>
								<entry key='IMA*' value='ET'/>
								<entry key='IMI*' value='ET'/>
								<entry key='IIN*' value='CT'/>
								</map>
							</node>

							<node name='groups'>
								<node name='ET'> <!-- Group Name -->
									<map>
										<entry key='description' value='Eastern Time Zone ATMs' />
										<entry key='priority' value='1' /><!--Priority in eips output file Name -->
										<entry key='stationNo' value='49' />
										<!-- Supported TM WorkType Examples for ATM :101, 102 ,103, 803 -->
										<entry key='pset' value='101' />
										<!-- Configuring what fields are used to define a unique batch 
											key -->
										<!-- For ex: <entry key='batchKey' value='User2+User3' /> -->
										<!-- For ex: <entry key='batchKey' value='SourceId' /> -->
										<entry key='batchKey' value='SourceLocation' />
										<entry key='exportPath' value='\\$1' />
										<entry key='customField3' value='09' />
										<entry key='customField5' value='85928' />
										<entry key='documentsGroup' value='defaultDocumentsGroup' />
										<entry key='holdoverDateSwitchTimeSchedule' value='default' />
										<entry key='generateDrn' value='true' />
										<entry key='site' value='site1' /> 			
										<entry key='region' value='region1' />		
										<entry key='currencyCodeFace' value='CAD' />
										<entry key='batchMaxItemCount' value='3000' /> <!-- number of items -->
										<entry key='batchMaxValue' value='150000' />
										<!-- SCER 2429  -->
										<entry key='putDeposit' value='true' />
										<entry key='wbiConfigNode' value='GroupDefaultWbiDepositNode' />
										<entry key='depositWorkType' value='ATMRemoteDeposit' />
										
										
										
										
										<!-- PSTC-2880 -->
										<entry key='itemTypeGroup' value='defaultItemTypeDefinition' /> 
										<!-- SCER 2644 Changes -->
										<entry key='sorterNumber' value='01' />
										
										<!-- PSTC-1918 -->
										<entry key='separateBatchPerDebitCreditItems' value='true' />
										<!--TGSR-427-->
										<entry key='displayBlankInEIPSWhenAmountZero' value='false' />	 
										
									</map>

									<!-- Sequences Configuration AT GROUP Level -->
									<node name='sequences'>
										<node name='ItemDrnSequence'>
											<map>
												<entry key='initialValue' value='1' />
												<entry key='maximumValue' value='9223372036854775806' />
												<entry key='incrementStep' value='1' />
												<entry key='rollOver' value='true' />
												<entry key='hardReset' value='9223372036854775807' />
												<entry key='resetTo' value='1' />
												<entry key='resetDRNDaily' value='true' />
												<entry key='numberOfValues' value='500' />
											</map>
										</node>
									</node>
								</node>
								<node name='CT'> <!-- Group -->
									<map>
										<entry key='description' value='Central Time Zone ATMs' />
										<entry key='priority' value='1' /><!--Priority in eips output file Name -->
										<entry key='stationNo' value='46' />
										<!-- Supported TM WorkType Examples for ATM :101, 102 ,103, 803 -->
										<entry key='pset' value='102' />
										<entry key='batchKey' value='SourceLocation' />
										<entry key='exportPath' value='\\$1' />
										<entry key='customField3' value='09' />
										<entry key='customField5' value='85928' />
										<entry key='documentsGroup' value='defaultDocumentsGroup' />
										<entry key='holdoverDateSwitchTimeSchedule' value='default' />
										<entry key='generateDrn' value='true' />
										<entry key='site' value='site1' /> 			
										<entry key='region' value='region1' />
										<entry key='currencyCodeFace' value='CAD' />	
										<entry key='batchMaxItemCount' value='3000' /> <!-- number of items -->
										<entry key='batchMaxValue' value='150000' />
										<!-- SCER 2429  -->
										<entry key='putDeposit' value='true' />
										<entry key='wbiConfigNode' value='GroupDefaultWbiDepositNode' />
										<entry key='depositWorkType' value='ATMRemoteDeposit' />
										
										<!-- PSTC-2880 -->
										<entry key='itemTypeGroup' value='defaultItemTypeDefinition' /> 
										<!-- SCER 2644 Changes -->
										<entry key='sorterNumber' value='01' />	
										<!-- PSTC-1918 -->
										<entry key='separateBatchPerDebitCreditItems' value='true' />
										<!--TGSR-427-->
										<entry key='displayBlankInEIPSWhenAmountZero' value='false' />		
											  

									</map>
									<!-- Sequences Configuration AT GROUP Level -->
									<node name='sequences'>
										<node name='ItemDrnSequence'>
											<map>
												<entry key='initialValue' value='1' />
												<entry key='maximumValue' value='9223372036854775806' />
												<entry key='incrementStep' value='1' />
												<entry key='rollOver' value='true' />
												<entry key='hardReset' value='9223372036854775807' />
												<entry key='resetTo' value='1' />
												<entry key='resetDRNDaily' value='true' />
												<entry key='numberOfValues' value='500' />
											</map>
										</node>
									</node>
								</node>
								<node name='MT'> <!-- Group Name -->
									<map>
										<entry key='description' value='Mountain Time Zone ATMs' />
										<entry key='priority' value='1' /><!--Priority in eips output file Name -->
										<entry key='stationNo' value='47' />
										<!-- Supported TM WorkType Examples for ATM :101, 102 ,103, 803 -->
										<entry key='pset' value='103' />
										<!-- Configuring what fields are used to define a unique batch 
											key -->
										<!-- For ex: <entry key='batchKey' value='User2+User3' /> -->
										<!-- For ex: <entry key='batchKey' value='SourceId' /> -->
										<entry key='batchKey' value='SourceLocation' />
										<entry key='exportPath' value='\\$1' />
										<entry key='customField3' value='09' />
										<entry key='customField5' value='85928' />
										<entry key='documentsGroup' value='defaultDocumentsGroup' />
										<entry key='holdoverDateSwitchTimeSchedule' value='default' />
										<entry key='generateDrn' value='true' />
										<entry key='site' value='site1' /> 			
										<entry key='region' value='region1' />
										<entry key='currencyCodeFace' value='CAD' />
										<entry key='batchMaxItemCount' value='3000' /> <!-- number of items -->
										<entry key='batchMaxValue' value='150000' />
										
										<!-- SCER 2429  -->
										<entry key='putDeposit' value='true' />
										<entry key='wbiConfigNode' value='GroupDefaultWbiDepositNode' />
										<entry key='depositWorkType' value='ATMRemoteDeposit' />
										
										<!-- PSTC-2880 -->
										<entry key='itemTypeGroup' value='defaultItemTypeDefinition' /> 
										<!-- SCER 2644 Changes -->
										<entry key='sorterNumber' value='01' />
										<!-- PSTC-1918 -->
										<entry key='separateBatchPerDebitCreditItems' value='false' />	
										<!--TGSR-427-->
										<entry key='displayBlankInEIPSWhenAmountZero' value='false' />	
											  

									</map>
									<node name='sequences'>
										<node name='ItemDrnSequence'>
											<map>
												<entry key='initialValue' value='1' />
												<entry key='maximumValue' value='9223372036854775806' />
												<entry key='incrementStep' value='1' />
												<entry key='rollOver' value='true' />
												<entry key='hardReset' value='9223372036854775807' />
												<entry key='resetTo' value='1' />
												<entry key='resetDRNDaily' value='true' />
												<entry key='numberOfValues' value='500' />
											</map>
										</node>
									</node>
								</node>
								<node name='PT'> <!-- Group Name -->
									<map>
										<entry key='description' value='Pacific Time Zone ATMs' />
										<entry key='priority' value='1' /><!--Priority in eips output file Name -->
										<entry key='stationNo' value='48' />
										<!-- Supported TM WorkType Examples for ATM :101, 102 ,103, 803 -->
										<entry key='pset' value='104' />
										<!-- Configuring what fields are used to define a unique batch 
											key -->
										<!-- For ex: <entry key='batchKey' value='User2+User3' /> -->
										<!-- For ex: <entry key='batchKey' value='SourceId' /> -->
										<entry key='batchKey' value='SourceLocation' />
										<entry key='exportPath' value='\\$1' />
										<entry key='customField3' value='09' />
										<entry key='customField5' value='85928' />
										<entry key='documentsGroup' value='defaultDocumentsGroup' />
										<entry key='holdoverDateSwitchTimeSchedule' value='default' />
										<entry key='generateDrn' value='true' />
										<entry key='site' value='site1' /> 			
										<entry key='region' value='region1' />
										<entry key='currencyCodeFace' value='CAD' />
										<entry key='batchMaxItemCount' value='3000' /> <!-- number of items -->
										<entry key='batchMaxValue' value='150000' />
										
										<!-- SCER 2429  -->
										<entry key='putDeposit' value='true' />
										<entry key='wbiConfigNode' value='GroupDefaultWbiDepositNode' />
										<entry key='depositWorkType' value='ATMRemoteDeposit' />
										
										<!-- PSTC-2880 -->
										<entry key='itemTypeGroup' value='defaultItemTypeDefinition' />
										<!-- SCER 2644 Changes -->
										<entry key='sorterNumber' value='01' />
										<!-- PSTC-1918 -->
										<entry key='separateBatchPerDebitCreditItems' value='true' />	
										<!--TGSR-427-->
										<entry key='displayBlankInEIPSWhenAmountZero' value='false' />	  

									</map>

									<!-- Sequences Configuration AT GROUP Level -->
									<node name='sequences'>
										<node name='ItemDrnSequence'>
											<map>
												<entry key='initialValue' value='1' />
												<entry key='maximumValue' value='9223372036854775806' />
												<entry key='incrementStep' value='1' />
												<entry key='rollOver' value='true' />
												<entry key='hardReset' value='9223372036854775807' />
												<entry key='resetTo' value='1' />
												<entry key='resetDRNDaily' value='true' />
												<entry key='numberOfValues' value='500' />
											</map>
										</node>
									</node>
								</node>
							</node>
							
							<!-- Sequences Configuration AT SOURCETYPE Level -->
							<node name='sequences'>
								<node name='ItemDrnSequence'>
									<map>
										<entry key='initialValue' value='1' />
										<entry key='maximumValue' value='9223372036854775806' />
										<entry key='incrementStep' value='1' />
										<entry key='rollOver' value='true' />
										<entry key='hardReset' value='9223372036854775807' />
										<entry key='resetTo' value='1' />
										<entry key='resetDRNDaily' value='true' />
										<entry key='numberOfValues' value='500' />
									</map>
								</node>
							</node>

						</node>
						<node name='thick_backoffice_or_commercial'>
						
										<!-- DRN Configuration - START-->
				<!--This drn formatting configuration will be used when the generateDrnDefault is set to false and the generateDrn is either set to false or not set for a particular group.-->
				<node name='drnConfig'>
					<!-- # DRN format is "ttrrttyyyymmddssss" # - rr is 2 digit region code 
						# - yyyymmdd is for the cycle date # - tttt is 4 digit station number # - 
						ssss is 4 digit sequence number -->
					<entry key='drn'
						value='{stationNumber,xstring,%r0r2sl}{regionCode,xstring,%l0l2sl}{str1}{str2}' />
					<node name='drn-parts'>
						<entry key='str1'
							value='{stationNumber,xstring,%l0l2sl}{cycleDate,date,yyyyMMdd}' />
						<entry key='str2' value='{nextDrnSequenceNumber,number,0000}' />
					</node>
				</node>
				
				<!-- This drn formatting configuration will be used when the generateDrnDefault is set to false and the generateDrn is set to true for a particular group.-->
				<node name='tcDrnConfig'>
					<!-- # DRN format is "ttrrttyyyymmddssss" # - rr is 2 digit region code 
						# - yyyymmdd is for the cycle date # - tttt is 4 digit station number # - 
						ssss is 4 digit sequence number -->
					<entry key='drn'
						value='{stationNumber,xstring,%r0r2sl}{regionCode,xstring,%l0l2sl}{str1}{str2}' />
					<node name='drn-parts'>
						<entry key='str1'
							value='{stationNumber,xstring,%l0l2sl}{cycleDate,date,yyyyMMdd}' />
						<entry key='str2' value='{nextDrnSequenceNumber,number,0000}' />
					</node>
				</node>
				<!--This config node will be used to format drn (for all the groups) when the generateDrnDefault is set to true.-->
				<!--Only If the generateDrnDefault is set to false,then this drnformat config will be used only for those groupswhose generatedrn is set to true.-->
				<node name='tcDrnFormat'>
					<!-- # DRN format is "ttrrttyyyymmddssss" # - rr is 2 digit region code 
						# - yyyymmdd is for the cycle date # - tttt is 4 digit station number # - 
						ssss is 4 digit sequence number -->
					<entry key='drn'
						value='{stationNumber,xstring,%r0r2sl}{regionCode,xstring,%l0l2sl}{str1}{str2}' />
					<node name='drn-parts'>
						<entry key='str1' value='00' />
						<entry key='str2' value='{nextDrnSequenceNumber,number,000000}' />
					</node>
				</node>
								
				
				<!-- DRN Configuration - END -->
						<entry key='BranchNumber' value='9999' />
						<entry key='priority' value='1' /><!--Priority in eips output file Name -->

							<map>
								<entry key='configKey' value='BatchSourceId' />
								<entry key='holdoverDateSwitchTimeSchedule' value='default' />
							</map>
							<node name='groupMapping'>
								<map>
									<entry key='777771' value='Group7' />
									<!--entry key='77777*' value='Group8' /-->
									<entry key='*' value='Group8' />
								</map>
							</node>

							<node name='groups'>
								<node name='Group7'> <!-- Group Name -->
									<map>
										<entry key='description' value='Group1 Capture Workstation Description' />
										<entry key='priority' value='1' /><!--Priority in eips output file Name -->
										<entry key='stationNo' value='1111' />
										<!-- Supported TM WorkType Examples for BRANCH :1,2,3,4,5,6,7,8,9,10 -->
										<entry key='pset' value='9' />
										<!--entry key='batchKey' value='BatchSourceId' / -->
										<entry key='exportPath' value='\\$1' />
										<entry key='customField1' value='10' />
										<entry key='customField2' value='435245' />
										<entry key='customField3' value='100' />
										<entry key='customField4' value='300' />
										<entry key='customField5' value='55555' />
										<entry key='documentsGroup' value='BranchDocumentsGroup' />
										<entry key='holdoverDateSwitchTimeSchedule' value='default' />
										<entry key='generateDrn' value='true' />
										
										<entry key='site' value='site1' /> 			
										<entry key='region' value='region1' />
										<entry key='currencyCodeFace' value='CAD' />		
										<entry key='batchMaxItemCount' value='3000' /> <!-- number of items -->
										<entry key='batchMaxValue' value='150000' />
										
										<!-- PSTC-2880 -->
										<entry key='itemTypeGroup' value='defaultItemTypeDefinition' /> 
										<!-- SCER 2644 Changes -->
										<entry key='sorterNumber' value='01' />
										<!--TGSR-427-->
										<entry key='displayBlankInEIPSWhenAmountZero' value='false' />	

									</map>

									<!-- Sequences Configuration AT GROUP Level -->
									<node name='sequences'>
										<node name='ItemDrnSequence'>
											<map>
												<entry key='initialValue' value='1' />
												<entry key='maximumValue' value='9223372036854775806' />
												<entry key='incrementStep' value='1' />
												<entry key='rollOver' value='true' />
												<entry key='hardReset' value='9223372036854775807' />
												<entry key='resetTo' value='1' />
												<entry key='resetDRNDaily' value='true' />
												<entry key='numberOfValues' value='500' />
											</map>
										</node>
									</node>

								</node>
								<node name='Group8'> <!-- Group -->
									<map>
										<entry key='description' value='Group2 Capture Workstation Description' />
										<entry key='priority' value='1' /><!--Priority in eips output file Name -->
										<entry key='stationNo' value='3333' />
										<!-- Supported TM WorkType Examples for BRANCH :1,2,3,4,5,6,7,8,9,10 -->
										<entry key='pset' value='10' />
										<entry key='batchKey' value='BatchSourceId' />
										<entry key='exportPath' value='\\$1' />
										<entry key='customField1' value='11' />
										<entry key='customField2' value='235245' />
										<entry key='customField3' value='200' />
										<entry key='customField4' value='500' />
										<entry key='customField5' value='75555' />
										<entry key='documentsGroup' value='BranchDocumentsGroup' />
										<entry key='holdoverDateSwitchTimeSchedule' value='default' />
										<entry key='generateDrn' value='true' />
										
										<entry key='site' value='site1' /> 			
										<entry key='region' value='region1' />
										<entry key='currencyCodeFace' value='CAD' />		
										<entry key='batchMaxItemCount' value='3000' /> <!-- number of items -->
										<entry key='batchMaxValue' value='150000' />
										
										<!-- PSTC-2880 -->
										<entry key='itemTypeGroup' value='defaultItemTypeDefinition' /> 
										<!-- SCER 2644 Changes -->
										<entry key='sorterNumber' value='01' />	
										<!--TGSR-427-->
										<entry key='displayBlankInEIPSWhenAmountZero' value='false' />	

									</map>

									<!-- Sequences Configuration AT GROUP Level -->
									<node name='sequences'>
										<node name='ItemDrnSequence'>
											<map>
												<entry key='initialValue' value='1' />
												<entry key='maximumValue' value='9223372036854775806' />
												<entry key='incrementStep' value='1' />
												<entry key='rollOver' value='true' />
												<entry key='hardReset' value='9223372036854775807' />
												<entry key='resetTo' value='1' />
												<entry key='resetDRNDaily' value='true' />
												<entry key='numberOfValues' value='500' />
											</map>
										</node>
									</node>

								</node>
							</node>
							
							<!-- Sequences Configuration AT SOURCETYPE Level -->
							<node name='sequences'>
								<node name='ItemDrnSequence'>
									<map>
										<entry key='initialValue' value='1' />
										<entry key='maximumValue' value='9223372036854775806' />
										<entry key='incrementStep' value='1' />
										<entry key='rollOver' value='true' />
										<entry key='hardReset' value='9223372036854775807' />
										<entry key='resetTo' value='1' />
										<entry key='resetDRNDaily' value='true' />
										<entry key='numberOfValues' value='500' />
									</map>
								</node>
							</node>

						</node>
						
						<node name='Commercial'>
						<entry key='BranchNumber' value='9999' />
						<entry key='priority' value='1' /><!--Priority in eips output file Name -->
							<map>
								<entry key='configKey' value='SourceId+LargeDeposit+User0+User1' />
								<entry key='holdoverDateSwitchTimeSchedule' value='default' />
							</map>
							<node name='groupMapping'>
								<map>
								<entry key='RDB+RegularDeposit+America\u002FNew\u005FYork+01' value='rdbEas' />
								<entry key='RDB+RegularDeposit+America\u002FChicago+01' value='rdbCen' />
								<entry key='RDB+RegularDeposit+America\u002FDenver+01' value='rdbMtn' />
								<entry key='RDB+RegularDeposit+America\u002FPhoenix+01' value='rdbArz' />
								<entry key='RDB+RegularDeposit+America\u002FLos\u005FAngeles+01' value='rdbPac' />
								<entry key='RDB+LargeDeposit+America\u002FNew\u005FYork+01' value='rdbLDEas' />
								<entry key='RDB+LargeDeposit+America\u002FChicago+01' value='rdbLDCen' />
								<entry key='RDB+LargeDeposit+America\u002FDenver+01' value='rdbLDMtn' />
								<entry key='RDB+LargeDeposit+America\u002FPhoenix+01' value='rdbLDArz' />
								<entry key='RDB+LargeDeposit+America\u002FLos\u005FAngeles+01' value='rdbLDPac' />
								</map>
							</node>

							<node name='groups'>
								<node name='rdbEas'> <!-- Group Name used for LargeDeposit if set to true -->
									<map>
										<entry key='description' value='RDB Eastern' />
										<entry key='priority' value='1' /><!--Priority in eips output file Name -->
										<entry key='stationNo' value='85' />
										<!-- Supported TM WorkType Examples for Commercial :111, 112, 113, 114, 132, 811, 131, 133, 834, 134 -->
										<entry key='pset' value='111' />
										<!-- Configuring what fields are used to define a unique batch 
											key -->
										<!-- For ex: <entry key='batchKey' value='User2+User3' /> -->
										<!-- For ex: <entry key='batchKey' value='SourceId' /> -->
										<entry key='batchKey' value='User1+User2+User3' />
										<entry key='exportPath' value='\\$1' />
										<entry key='documentsGroup' value='defaultDocumentsGroup' />
										<entry key='holdoverDateSwitchTimeSchedule' value='default' />
										<entry key='generateDrn' value='true' />
										<entry key='site' value='site1' /> 			
										<entry key='region' value='region1' />
										<entry key='currencyCodeFace' value='CAD' />		
										<entry key='batchMaxItemCount' value='500' /> <!-- number of items -->
										<entry key='batchMaxValue' value='150000' />
										
										<!-- PSTC-2880 -->
										<entry key='itemTypeGroup' value='defaultItemTypeDefinition' /> 
										<!-- SCER 2644 Changes -->
										<entry key='sorterNumber' value='01' />										
										<!--TGSR-427-->
										<entry key='displayBlankInEIPSWhenAmountZero' value='false' />									
										
									</map>

									<!-- Sequences Configuration AT GROUP Level -->
									<node name='sequences'>
										<node name='ItemDrnSequence'>
											<map>
												<entry key='initialValue' value='1' />
												<entry key='maximumValue' value='9223372036854775806' />
												<entry key='incrementStep' value='1' />
												<entry key='rollOver' value='true' />
												<entry key='hardReset' value='9223372036854775807' />
												<entry key='resetTo' value='1' />
												<entry key='resetDRNDaily' value='true' />
												<entry key='numberOfValues' value='500' />
											</map>
										</node>
									</node>

								</node>
								<node name='rdbCen'> <!-- Group Name used for LargeDeposit if set to true -->
									<map>
										<entry key='description' value='RDB Central' />
										<entry key='priority' value='1' /><!--Priority in eips output file Name -->
										<entry key='stationNo' value='86' />
										<!-- Supported TM WorkType Examples for Commercial :111, 112, 113, 114, 132, 811, 131, 133, 834, 134 -->
										<entry key='pset' value='112' />
										<!-- Configuring what fields are used to define a unique batch 
											key -->
										<!-- For ex: <entry key='batchKey' value='User2+User3' /> -->
										<!-- For ex: <entry key='batchKey' value='SourceId' /> -->
										<entry key='batchKey' value='User1+User2+User3' />
										<entry key='exportPath' value='\\$1' />										
										<entry key='documentsGroup' value='defaultDocumentsGroup' />
										<entry key='holdoverDateSwitchTimeSchedule' value='default' />
										<entry key='generateDrn' value='true' />
										<entry key='site' value='site1' /> 			
										<entry key='region' value='region1' />
										<entry key='currencyCodeFace' value='CAD' />		
										<entry key='batchMaxItemCount' value='3000' /> <!-- number of items -->
										<entry key='batchMaxValue' value='150000' />
										
										<!-- PSTC-2880 -->
										<entry key='itemTypeGroup' value='defaultItemTypeDefinition' /> 
										<!-- SCER 2644 Changes -->
										<entry key='sorterNumber' value='01' />	
										<!--TGSR-427-->
										<entry key='displayBlankInEIPSWhenAmountZero' value='false' />	

									</map>

									<!-- Sequences Configuration AT GROUP Level -->
									<node name='sequences'>
										<node name='ItemDrnSequence'>
											<map>
												<entry key='initialValue' value='1' />
												<entry key='maximumValue' value='9223372036854775806' />
												<entry key='incrementStep' value='1' />
												<entry key='rollOver' value='true' />
												<entry key='hardReset' value='9223372036854775807' />
												<entry key='resetTo' value='1' />
												<entry key='resetDRNDaily' value='true' />
												<entry key='numberOfValues' value='500' />
											</map>
										</node>
									</node>
								</node>
								<node name='rdbMtn'> <!-- Group Name used for LargeDeposit if set to true -->
									<map>
										<entry key='description' value='RDB Mountain' />
										<entry key='priority' value='1' /><!--Priority in eips output file Name -->
										<entry key='stationNo' value='87' />
										<!-- Supported TM WorkType Examples for Commercial :111, 112, 113, 114, 132, 811, 131, 133, 834, 134 -->
										<entry key='pset' value='113' />
										<!-- Configuring what fields are used to define a unique batch 
											key -->
										<!-- For ex: <entry key='batchKey' value='User2+User3' /> -->
										<!-- For ex: <entry key='batchKey' value='SourceId' /> -->
										<entry key='batchKey' value='User1+User2+User3' />
										<entry key='exportPath' value='\\$1' />										
										<entry key='documentsGroup' value='defaultDocumentsGroup' />
										<entry key='holdoverDateSwitchTimeSchedule' value='default' />
										<entry key='generateDrn' value='true' />
										<entry key='site' value='site1' /> 			
										<entry key='region' value='region1' />
										<entry key='currencyCodeFace' value='CAD' />
										<entry key='batchMaxItemCount' value='3000' /> <!-- number of items -->
										<entry key='batchMaxValue' value='150000' />
										
										<!-- PSTC-2880 -->
										<entry key='itemTypeGroup' value='defaultItemTypeDefinition' /> 
										<!--TGSR-427-->
										<entry key='displayBlankInEIPSWhenAmountZero' value='false' />	
									</map>

									<!-- Sequences Configuration AT GROUP Level -->
									<node name='sequences'>
										<node name='ItemDrnSequence'>
											<map>
												<entry key='initialValue' value='1' />
												<entry key='maximumValue' value='9223372036854775806' />
												<entry key='incrementStep' value='1' />
												<entry key='rollOver' value='true' />
												<entry key='hardReset' value='9223372036854775807' />
												<entry key='resetTo' value='1' />
												<entry key='resetDRNDaily' value='true' />
												<entry key='numberOfValues' value='500' />
											</map>
										</node>
									</node>
								</node>
								<node name='rdbArz'> <!-- Group Name used for LargeDeposit if set to true -->
									<map>
										<entry key='description' value='RDB Arizona' />
										<entry key='priority' value='1' /><!--Priority in eips output file Name -->
										<entry key='stationNo' value='88' />
										<!-- Supported TM WorkType Examples for Commercial :111, 112, 113, 114, 132, 811, 131, 133, 834, 134 -->
										<entry key='pset' value='913' />
										<!-- Configuring what fields are used to define a unique batch 
											key -->
										<!-- For ex: <entry key='batchKey' value='User2+User3' /> -->
										<!-- For ex: <entry key='batchKey' value='SourceId' /> -->
										<entry key='batchKey' value='User1+User2+User3' />
										<entry key='exportPath' value='\\$1' />					
										<entry key='documentsGroup' value='defaultDocumentsGroup' />
										<entry key='holdoverDateSwitchTimeSchedule' value='default' />
										<entry key='generateDrn' value='true' />
										<entry key='site' value='site1' /> 			
										<entry key='region' value='region1' />
										<entry key='currencyCodeFace' value='CAD' />
										<entry key='batchMaxItemCount' value='3000' /> <!-- number of items -->
										<entry key='batchMaxValue' value='150000' />
										
										<!-- PSTC-2880 -->
										<entry key='itemTypeGroup' value='defaultItemTypeDefinition' /> 
										<!-- SCER 2644 Changes -->
										<entry key='sorterNumber' value='01' />
										<!--TGSR-427-->
										<entry key='displayBlankInEIPSWhenAmountZero' value='false' />	
									</map>
									<!-- Sequences Configuration AT GROUP Level -->
									<node name='sequences'>
										<node name='ItemDrnSequence'>
											<map>
												<entry key='initialValue' value='1' />
												<entry key='maximumValue' value='9223372036854775806' />
												<entry key='incrementStep' value='1' />
												<entry key='rollOver' value='true' />
												<entry key='hardReset' value='9223372036854775807' />
												<entry key='resetTo' value='1' />
												<entry key='resetDRNDaily' value='true' />
												<entry key='numberOfValues' value='500' />
											</map>
										</node>
									</node>
								</node>
								<node name='rdbPac'> <!-- Group Name used for LargeDeposit if set to true -->
									<map>
										<entry key='description' value='RDB Pacific' />
										<entry key='priority' value='1' /><!--Priority in eips output file Name -->
										<entry key='stationNo' value='89' />
										<!-- Supported TM WorkType Examples for Commercial :111, 112, 113, 114, 132, 811, 131, 133, 834, 134 -->
										<entry key='pset' value='114' />
										<!-- Configuring what fields are used to define a unique batch 
											key -->
										<!-- For ex: <entry key='batchKey' value='User2+User3' /> -->
										<!-- For ex: <entry key='batchKey' value='SourceId' /> -->
										<entry key='batchKey' value='User1+User2+User3' />
										<entry key='exportPath' value='\\$1' />					
										<entry key='documentsGroup' value='defaultDocumentsGroup' />
										<entry key='holdoverDateSwitchTimeSchedule' value='default' />
										<entry key='generateDrn' value='true' />
										<entry key='site' value='site1' /> 			
										<entry key='region' value='region1' />
										<entry key='currencyCodeFace' value='CAD' />
										<entry key='batchMaxItemCount' value='3000' /> <!-- number of items -->
										<entry key='batchMaxValue' value='150000' />
										
										<!-- PSTC-2880 -->
										<entry key='itemTypeGroup' value='defaultItemTypeDefinition' /> 
										<!-- SCER 2644 Changes -->
										<entry key='sorterNumber' value='01' />
										<!--TGSR-427-->
										<entry key='displayBlankInEIPSWhenAmountZero' value='false' />	

									</map>
									<!-- Sequences Configuration AT GROUP Level -->
									<node name='sequences'>
										<node name='ItemDrnSequence'>
											<map>
												<entry key='initialValue' value='1' />
												<entry key='maximumValue' value='9223372036854775806' />
												<entry key='incrementStep' value='1' />
												<entry key='rollOver' value='true' />
												<entry key='hardReset' value='9223372036854775807' />
												<entry key='resetTo' value='1' />
												<entry key='resetDRNDaily' value='true' />
												<entry key='numberOfValues' value='500' />
											</map>
										</node>
									</node>
								</node>
								<node name='rdbCARTet'> <!-- Group Name used for LargeDeposit if set to true -->
									<map>
										<entry key='description' value='RDB CART Eastern' />
										<entry key='priority' value='1' /><!--Priority in eips output file Name -->
										<entry key='stationNo' value='56' />
										<!-- Supported TM WorkType Examples for Commercial :111, 112, 113, 114, 132, 811, 131, 133, 834, 134 -->
										<entry key='pset' value='111' />
										<!-- Configuring what fields are used to define a unique batch 
											key -->
										<!-- For ex: <entry key='batchKey' value='User2+User3' /> -->
										<!-- For ex: <entry key='batchKey' value='SourceId' /> -->
										<entry key='batchKey' value='User1+User2+User3' />
										<entry key='exportPath' value='\\$1' />										
										<entry key='documentsGroup' value='defaultDocumentsGroup' />
										<entry key='holdoverDateSwitchTimeSchedule' value='default' />
										<entry key='generateDrn' value='true' />
										<entry key='site' value='site1' /> 			
										<entry key='region' value='region1' />
										<entry key='currencyCodeFace' value='CAD' />
										<entry key='batchMaxItemCount' value='3000' /> <!-- number of items -->
										<entry key='batchMaxValue' value='150000' />
										
										<!-- PSTC-2880 -->
										<entry key='itemTypeGroup' value='defaultItemTypeDefinition' /> 
										<!-- SCER 2644 Changes -->
										<entry key='sorterNumber' value='01' />
										<!--TGSR-427-->
										<entry key='displayBlankInEIPSWhenAmountZero' value='false' />	

									</map>
									<!-- Sequences Configuration AT GROUP Level -->
									<node name='sequences'>
										<node name='ItemDrnSequence'>
											<map>
												<entry key='initialValue' value='1' />
												<entry key='maximumValue' value='9223372036854775806' />
												<entry key='incrementStep' value='1' />
												<entry key='rollOver' value='true' />
												<entry key='hardReset' value='9223372036854775807' />
												<entry key='resetTo' value='1' />
												<entry key='resetDRNDaily' value='true' />
												<entry key='numberOfValues' value='500' />
											</map>
										</node>
									</node>
								</node>
								<node name='rdbCARTct'> <!-- Group Name used for LargeDeposit if set to true -->
									<map>
										<entry key='description' value='RDB CART Central' />
										<entry key='priority' value='1' /><!--Priority in eips output file Name -->
										<entry key='stationNo' value='57' />
										<!-- Supported TM WorkType Examples for Commercial :111, 112, 113, 114, 132, 811, 131, 133, 834, 134 -->
										<entry key='pset' value='112' />
										<!-- Configuring what fields are used to define a unique batch 
											key -->
										<!-- For ex: <entry key='batchKey' value='User2+User3' /> -->
										<!-- For ex: <entry key='batchKey' value='SourceId' /> -->
										<entry key='batchKey' value='User1+User2+User3' />
										<entry key='exportPath' value='\\$1' />
										<entry key='customField1' value='10' />										
										<entry key='documentsGroup' value='defaultDocumentsGroup' />
										<entry key='holdoverDateSwitchTimeSchedule' value='default' />
										<entry key='generateDrn' value='true' />
										<entry key='site' value='site1' /> 			
										<entry key='region' value='region1' />
										<entry key='currencyCodeFace' value='CAD' />
										<entry key='batchMaxItemCount' value='3000' /> <!-- number of items -->
										<entry key='batchMaxValue' value='150000' />
										
										<!-- PSTC-2880 -->
										<entry key='itemTypeGroup' value='defaultItemTypeDefinition' /> 
										<!-- SCER 2644 Changes -->
										<entry key='sorterNumber' value='01' />
										<!--TGSR-427-->
										<entry key='displayBlankInEIPSWhenAmountZero' value='false' />	

									</map>
									<!-- Sequences Configuration AT GROUP Level -->
									<node name='sequences'>
										<node name='ItemDrnSequence'>
											<map>
												<entry key='initialValue' value='1' />
												<entry key='maximumValue' value='9223372036854775806' />
												<entry key='incrementStep' value='1' />
												<entry key='rollOver' value='true' />
												<entry key='hardReset' value='9223372036854775807' />
												<entry key='resetTo' value='1' />
												<entry key='resetDRNDaily' value='true' />
												<entry key='numberOfValues' value='500' />
											</map>
										</node>
									</node>
								</node>
								<node name='rdbCARTmt'> <!-- Group Name used for LargeDeposit if set to true -->
									<map>
										<entry key='description' value='RDB CART Mountain' />
										<entry key='priority' value='1' /><!--Priority in eips output file Name -->
										<entry key='stationNo' value='58' />
										<!-- Supported TM WorkType Examples for Commercial :111, 112, 113, 114, 132, 811, 131, 133, 834, 134 -->
										<entry key='pset' value='113' />
										<!-- Configuring what fields are used to define a unique batch 
											key -->
										<!-- For ex: <entry key='batchKey' value='User2+User3' /> -->
										<!-- For ex: <entry key='batchKey' value='SourceId' /> -->
										<entry key='batchKey' value='User1+User2+User3' />
										<entry key='exportPath' value='\\$1' />										
										<entry key='documentsGroup' value='defaultDocumentsGroup' />
										<entry key='holdoverDateSwitchTimeSchedule' value='default' />
										<entry key='generateDrn' value='true' />
										<entry key='site' value='site1' /> 			
										<entry key='region' value='region1' />
										<entry key='currencyCodeFace' value='CAD' />
										<entry key='batchMaxItemCount' value='3000' /> <!-- number of items -->
										<entry key='batchMaxValue' value='150000' />
										
										<!-- PSTC-2880 -->
										<entry key='itemTypeGroup' value='defaultItemTypeDefinition' /> 
										<!-- SCER 2644 Changes -->
										<entry key='sorterNumber' value='01' />
										<!--TGSR-427-->
										<entry key='displayBlankInEIPSWhenAmountZero' value='false' />	

									</map>
									<!-- Sequences Configuration AT GROUP Level -->
									<node name='sequences'>
										<node name='ItemDrnSequence'>
											<map>
												<entry key='initialValue' value='1' />
												<entry key='maximumValue' value='9223372036854775806' />
												<entry key='incrementStep' value='1' />
												<entry key='rollOver' value='true' />
												<entry key='hardReset' value='9223372036854775807' />
												<entry key='resetTo' value='1' />
												<entry key='resetDRNDaily' value='true' />
												<entry key='numberOfValues' value='500' />
											</map>
										</node>
									</node>
								</node>
								<node name='rdbCARTar'> <!-- Group Name used for LargeDeposit if set to true -->
									<map>
										<entry key='description' value='RDB CART Arizona' />
										<entry key='priority' value='1' /><!--Priority in eips output file Name -->
										<entry key='stationNo' value='59' />
										<!-- Supported TM WorkType Examples for Commercial :111, 112, 113, 114, 132, 811, 131, 133, 834, 134 -->
										<entry key='pset' value='913' />
										<!-- Configuring what fields are used to define a unique batch 
											key -->
										<!-- For ex: <entry key='batchKey' value='User2+User3' /> -->
										<!-- For ex: <entry key='batchKey' value='SourceId' /> -->
										<entry key='batchKey' value='User1+User2+User3' />
										<entry key='exportPath' value='\\$1' />										
										<entry key='documentsGroup' value='defaultDocumentsGroup' />
										<entry key='holdoverDateSwitchTimeSchedule' value='default' />
										<entry key='generateDrn' value='true' />
										<entry key='site' value='site1' /> 			
										<entry key='region' value='region1' />
										<entry key='currencyCodeFace' value='CAD' />
										<entry key='batchMaxItemCount' value='3000' /> <!-- number of items -->
										<entry key='batchMaxValue' value='150000' />
										
										<!-- PSTC-2880 -->
										<entry key='itemTypeGroup' value='defaultItemTypeDefinition' /> 
										<!-- SCER 2644 Changes -->
										<entry key='sorterNumber' value='01' />
										<!--TGSR-427-->
										<entry key='displayBlankInEIPSWhenAmountZero' value='false' />	

									</map>
									<!-- Sequences Configuration AT GROUP Level -->
									<node name='sequences'>
										<node name='ItemDrnSequence'>
											<map>
												<entry key='initialValue' value='1' />
												<entry key='maximumValue' value='9223372036854775806' />
												<entry key='incrementStep' value='1' />
												<entry key='rollOver' value='true' />
												<entry key='hardReset' value='9223372036854775807' />
												<entry key='resetTo' value='1' />
												<entry key='resetDRNDaily' value='true' />
												<entry key='numberOfValues' value='500' />
											</map>
										</node>
									</node>
								</node>
								<node name='rdbCARTpt'> <!-- Group Name used for LargeDeposit if set to true -->
									<map>
										<entry key='description' value='RDB CART Pacific' />
										<entry key='priority' value='1' /><!--Priority in eips output file Name -->
										<entry key='stationNo' value='50' />
										<!-- Supported TM WorkType Examples for Commercial :111, 112, 113, 114, 132, 811, 131, 133, 834, 134 -->
										<entry key='pset' value='114' />
										<!-- Configuring what fields are used to define a unique batch 
											key -->
										<!-- For ex: <entry key='batchKey' value='User2+User3' /> -->
										<!-- For ex: <entry key='batchKey' value='SourceId' /> -->
										<entry key='batchKey' value='User1+User2+User3' />
										<entry key='exportPath' value='\\$1' />										
										<entry key='documentsGroup' value='defaultDocumentsGroup' />
										<entry key='holdoverDateSwitchTimeSchedule' value='default' />
										<entry key='generateDrn' value='true' />
										<entry key='site' value='site1' /> 			
										<entry key='region' value='region1' />
										<entry key='currencyCodeFace' value='CAD' />
										<entry key='batchMaxItemCount' value='3000' /> <!-- number of items -->
										<entry key='batchMaxValue' value='150000' />
										
										<!-- PSTC-2880 -->
										<entry key='itemTypeGroup' value='defaultItemTypeDefinition' /> 
										<!-- SCER 2644 Changes -->
										<entry key='sorterNumber' value='01' />
										<!--TGSR-427-->
										<entry key='displayBlankInEIPSWhenAmountZero' value='false' />	

									</map>
									<!-- Sequences Configuration AT GROUP Level -->
									<node name='sequences'>
										<node name='ItemDrnSequence'>
											<map>
												<entry key='initialValue' value='1' />
												<entry key='maximumValue' value='9223372036854775806' />
												<entry key='incrementStep' value='1' />
												<entry key='rollOver' value='true' />
												<entry key='hardReset' value='9223372036854775807' />
												<entry key='resetTo' value='1' />
												<entry key='resetDRNDaily' value='true' />
												<entry key='numberOfValues' value='500' />
											</map>
										</node>
									</node>
								</node>
								<node name='rdbLDEas'> <!-- Group Name used for LargeDeposit if set to true -->
									<map>
										<entry key='description' value='rdbLD Eastern' />
										<entry key='priority' value='1' /><!--Priority in eips output file Name -->
										<entry key='stationNo' value='82' />
										<!-- Supported TM WorkType Examples for Commercial :111, 112, 113, 114, 132, 811, 131, 133, 834, 134 -->
										<entry key='pset' value='811' />
										<!-- Configuring what fields are used to define a unique batch 
											key -->
										<!-- For ex: <entry key='batchKey' value='User2+User3' /> -->
										<!-- For ex: <entry key='batchKey' value='SourceId' /> -->
										<entry key='batchKey' value='User1+User2+User3' />
										<entry key='exportPath' value='\\$1' />										
										<entry key='documentsGroup' value='defaultDocumentsGroup' />
										<entry key='holdoverDateSwitchTimeSchedule' value='default' />
										<entry key='generateDrn' value='true' />
										<entry key='site' value='site1' /> 			
										<entry key='region' value='region1' />
										<entry key='currencyCodeFace' value='CAD' />
										<entry key='batchMaxItemCount' value='3000' /> <!-- number of items -->
										<entry key='batchMaxValue' value='150000' />
										
										<!-- PSTC-2880 -->
										<entry key='itemTypeGroup' value='defaultItemTypeDefinition' /> 
										<!-- SCER 2644 Changes -->
										<entry key='sorterNumber' value='01' />
										
															<!-- PSTC-1918 -->
										<entry key='separateBatchPerDebitCreditItems' value='false' />
										<!--TGSR-427-->
										<entry key='displayBlankInEIPSWhenAmountZero' value='false' />	
											 

									</map>
									<!-- Sequences Configuration AT GROUP Level -->
									<node name='sequences'>
										<node name='ItemDrnSequence'>
											<map>
												<entry key='initialValue' value='1' />
												<entry key='maximumValue' value='9223372036854775806' />
												<entry key='incrementStep' value='1' />
												<entry key='rollOver' value='true' />
												<entry key='hardReset' value='9223372036854775807' />
												<entry key='resetTo' value='1' />
												<entry key='resetDRNDaily' value='true' />
												<entry key='numberOfValues' value='500' />
											</map>
										</node>
									</node>
								</node>
								<node name='rdbLDCen'> <!-- Group Name used for LargeDeposit if set to true -->
									<map>
										<entry key='description' value='rdbLD Central' />
										<entry key='priority' value='1' /><!--Priority in eips output file Name -->
										<entry key='stationNo' value='83' />
										<!-- Supported TM WorkType Examples for Commercial :111, 112, 113, 114, 132, 811, 131, 133, 834, 134 -->
										<entry key='pset' value='812' />
										<!-- Configuring what fields are used to define a unique batch 
											key -->
										<!-- For ex: <entry key='batchKey' value='User2+User3' /> -->
										<!-- For ex: <entry key='batchKey' value='SourceId' /> -->
										<entry key='batchKey' value='User1+User2+User3' />
										<entry key='exportPath' value='\\$1' />										
										<entry key='documentsGroup' value='defaultDocumentsGroup' />
										<entry key='holdoverDateSwitchTimeSchedule' value='default' />
										<entry key='generateDrn' value='true' />
										<entry key='site' value='site1' /> 			
										<entry key='region' value='region1' />
										<entry key='currencyCodeFace' value='CAD' />
										<entry key='batchMaxItemCount' value='3000' /> <!-- number of items -->
										<entry key='batchMaxValue' value='150000' />
										
										<!-- PSTC-2880 -->
										<entry key='itemTypeGroup' value='defaultItemTypeDefinition' /> 
										<!-- SCER 2644 Changes -->
										<entry key='sorterNumber' value='01' />
										<!--TGSR-427-->
										<entry key='displayBlankInEIPSWhenAmountZero' value='false' />	

									</map>
									<!-- Sequences Configuration AT GROUP Level -->
									<node name='sequences'>
										<node name='ItemDrnSequence'>
											<map>
												<entry key='initialValue' value='1' />
												<entry key='maximumValue' value='9223372036854775806' />
												<entry key='incrementStep' value='1' />
												<entry key='rollOver' value='true' />
												<entry key='hardReset' value='9223372036854775807' />
												<entry key='resetTo' value='1' />
												<entry key='resetDRNDaily' value='true' />
												<entry key='numberOfValues' value='500' />
											</map>
										</node>
									</node>
								</node>
								<node name='rdbLDMtn'> <!-- Group Name used for LargeDeposit if set to true -->
									<map>
										<entry key='description' value='rdbLD Mountain' />
										<entry key='priority' value='1' /><!--Priority in eips output file Name -->
										<entry key='stationNo' value='84' />
										<!-- Supported TM WorkType Examples for Commercial :111, 112, 113, 114, 132, 811, 131, 133, 834, 134 -->
										<entry key='pset' value='813' />
										<!-- Configuring what fields are used to define a unique batch 
											key -->
										<!-- For ex: <entry key='batchKey' value='User2+User3' /> -->
										<!-- For ex: <entry key='batchKey' value='SourceId' /> -->
										<entry key='batchKey' value='User1+User2+User3' />
										<entry key='exportPath' value='\\$1' />										
										<entry key='documentsGroup' value='defaultDocumentsGroup' />
										<entry key='holdoverDateSwitchTimeSchedule' value='default' />
										<entry key='generateDrn' value='true' />
										<entry key='site' value='site1' /> 			
										<entry key='region' value='region1' />
										<entry key='currencyCodeFace' value='CAD' />
										<entry key='batchMaxItemCount' value='3000' /> <!-- number of items -->
										<entry key='batchMaxValue' value='150000' />
										
										<!-- PSTC-2880 -->
										<entry key='itemTypeGroup' value='defaultItemTypeDefinition' /> 
										<!-- SCER 2644 Changes -->
										<entry key='sorterNumber' value='01' />
										<!--TGSR-427-->
										<entry key='displayBlankInEIPSWhenAmountZero' value='false' />	

									</map>
									<!-- Sequences Configuration AT GROUP Level -->
									<node name='sequences'>
										<node name='ItemDrnSequence'>
											<map>
												<entry key='initialValue' value='1' />
												<entry key='maximumValue' value='9223372036854775806' />
												<entry key='incrementStep' value='1' />
												<entry key='rollOver' value='true' />
												<entry key='hardReset' value='9223372036854775807' />
												<entry key='resetTo' value='1' />
												<entry key='resetDRNDaily' value='true' />
												<entry key='numberOfValues' value='500' />
											</map>
										</node>
									</node>
								</node>
								<node name='rdbLDArz'> <!-- Group Name used for LargeDeposit if set to true -->
									<map>
										<entry key='description' value='rdbLD Arizona' />
										<entry key='priority' value='1' /><!--Priority in eips output file Name -->
										<entry key='stationNo' value='65' />
										<!-- Supported TM WorkType Examples for Commercial :111, 112, 113, 114, 132, 811, 131, 133, 834, 134 -->
										<entry key='pset' value='713' />
										<!-- Configuring what fields are used to define a unique batch 
											key -->
										<!-- For ex: <entry key='batchKey' value='User2+User3' /> -->
										<!-- For ex: <entry key='batchKey' value='SourceId' /> -->
										<entry key='batchKey' value='User1+User2+User3' />
										<entry key='exportPath' value='\\$1' />										
										<entry key='documentsGroup' value='defaultDocumentsGroup' />
										<entry key='holdoverDateSwitchTimeSchedule' value='default' />
										<entry key='generateDrn' value='true' />
										<entry key='site' value='site1' /> 			
										<entry key='region' value='region1' />
										<entry key='currencyCodeFace' value='CAD' />
										<entry key='batchMaxItemCount' value='3000' /> <!-- number of items -->
										<entry key='batchMaxValue' value='150000' />
										
										<!-- PSTC-2880 -->
										<entry key='itemTypeGroup' value='defaultItemTypeDefinition' /> 
										<!-- SCER 2644 Changes -->
										<entry key='sorterNumber' value='01' />
										<!--TGSR-427-->
										<entry key='displayBlankInEIPSWhenAmountZero' value='false' />	

									</map>
									<!-- Sequences Configuration AT GROUP Level -->
									<node name='sequences'>
										<node name='ItemDrnSequence'>
											<map>
												<entry key='initialValue' value='1' />
												<entry key='maximumValue' value='9223372036854775806' />
												<entry key='incrementStep' value='1' />
												<entry key='rollOver' value='true' />
												<entry key='hardReset' value='9223372036854775807' />
												<entry key='resetTo' value='1' />
												<entry key='resetDRNDaily' value='true' />
												<entry key='numberOfValues' value='500' />
											</map>
										</node>
									</node>
								</node>
								<node name='rdbLDPac'> <!-- Group Name used for LargeDeposit if set to true -->
									<map>
										<entry key='description' value='rdbLD Pacific' />
										<entry key='priority' value='1' /><!--Priority in eips output file Name -->
										<entry key='stationNo' value='61' />
										<!-- Supported TM WorkType Examples for Commercial :111, 112, 113, 114, 132, 811, 131, 133, 834, 134 -->
										<entry key='pset' value='814' />
										<!-- Configuring what fields are used to define a unique batch 
											key -->
										<!-- For ex: <entry key='batchKey' value='User2+User3' /> -->
										<!-- For ex: <entry key='batchKey' value='SourceId' /> -->
										<entry key='batchKey' value='User1+User2+User3' />
										<entry key='exportPath' value='\\$1' />										
										<entry key='documentsGroup' value='defaultDocumentsGroup' />
										<entry key='holdoverDateSwitchTimeSchedule' value='default' />
										<entry key='generateDrn' value='true' />
										<entry key='site' value='site1' /> 			
										<entry key='region' value='region1' />
										<entry key='currencyCodeFace' value='CAD' />
										<entry key='batchMaxItemCount' value='3000' /> <!-- number of items -->
										<entry key='batchMaxValue' value='150000' />
										
										<!-- PSTC-2880 -->
										<entry key='itemTypeGroup' value='defaultItemTypeDefinition' /> 
										<!-- SCER 2644 Changes -->
										<entry key='sorterNumber' value='01' />
										<!--TGSR-427-->
										<entry key='displayBlankInEIPSWhenAmountZero' value='false' />	

									</map>
									<!-- Sequences Configuration AT GROUP Level -->
									<node name='sequences'>
										<node name='ItemDrnSequence'>
											<map>
												<entry key='initialValue' value='1' />
												<entry key='maximumValue' value='9223372036854775806' />
												<entry key='incrementStep' value='1' />
												<entry key='rollOver' value='true' />
												<entry key='hardReset' value='9223372036854775807' />
												<entry key='resetTo' value='1' />
												<entry key='resetDRNDaily' value='true' />
												<entry key='numberOfValues' value='500' />
											</map>
										</node>
									</node>
								</node>
								<node name='rdbLDCARTet'> <!-- Group Name used for LargeDeposit if set to true -->
									<map>
										<entry key='description' value='rdbLD CART Eastern' />
										<entry key='priority' value='1' /><!--Priority in eips output file Name -->
										<entry key='stationNo' value='51' />
										<!-- Supported TM WorkType Examples for Commercial :111, 112, 113, 114, 132, 811, 131, 133, 834, 134 -->
										<entry key='pset' value='811' />
										<!-- Configuring what fields are used to define a unique batch 
											key -->
										<!-- For ex: <entry key='batchKey' value='User2+User3' /> -->
										<!-- For ex: <entry key='batchKey' value='SourceId' /> -->
										<entry key='batchKey' value='User1+User2+User3' />
										<entry key='exportPath' value='\\$1' />										
										<entry key='documentsGroup' value='defaultDocumentsGroup' />
										<entry key='holdoverDateSwitchTimeSchedule' value='default' />
										<entry key='generateDrn' value='true' />
										<entry key='site' value='site1' /> 			
										<entry key='region' value='region1' />
										<entry key='currencyCodeFace' value='CAD' />
										<entry key='batchMaxItemCount' value='3000' /> <!-- number of items -->
										<entry key='batchMaxValue' value='150000' />
										
										<!-- PSTC-2880 -->
										<entry key='itemTypeGroup' value='defaultItemTypeDefinition' /> 
										<!-- SCER 2644 Changes -->
										<entry key='sorterNumber' value='01' />
										<!--TGSR-427-->
										<entry key='displayBlankInEIPSWhenAmountZero' value='false' />	

									</map>
									<!-- Sequences Configuration AT GROUP Level -->
									<node name='sequences'>
										<node name='ItemDrnSequence'>
											<map>
												<entry key='initialValue' value='1' />
												<entry key='maximumValue' value='9223372036854775806' />
												<entry key='incrementStep' value='1' />
												<entry key='rollOver' value='true' />
												<entry key='hardReset' value='9223372036854775807' />
												<entry key='resetTo' value='1' />
												<entry key='resetDRNDaily' value='true' />
												<entry key='numberOfValues' value='500' />
											</map>
										</node>
									</node>
								</node>
								<node name='rdbLDCARTct'> <!-- Group Name used for LargeDeposit if set to true -->
									<map>
										<entry key='description' value='rdbLD CART Central' />
										<entry key='priority' value='1' /><!--Priority in eips output file Name -->
										<entry key='stationNo' value='52' />
										<!-- Supported TM WorkType Examples for Commercial :111, 112, 113, 114, 132, 811, 131, 133, 834, 134 -->
										<entry key='pset' value='812' />
										<!-- Configuring what fields are used to define a unique batch 
											key -->
										<!-- For ex: <entry key='batchKey' value='User2+User3' /> -->
										<!-- For ex: <entry key='batchKey' value='SourceId' /> -->
										<entry key='batchKey' value='User1+User2+User3' />
										<entry key='exportPath' value='\\$1' />										
										<entry key='documentsGroup' value='defaultDocumentsGroup' />
										<entry key='holdoverDateSwitchTimeSchedule' value='default' />
										<entry key='generateDrn' value='true' />
										<entry key='site' value='site1' /> 			
										<entry key='region' value='region1' />
										<entry key='currencyCodeFace' value='CAD' />
										<entry key='batchMaxItemCount' value='3000' /> <!-- number of items -->
										<entry key='batchMaxValue' value='150000' />
										
										<!-- PSTC-2880 -->
										<entry key='itemTypeGroup' value='defaultItemTypeDefinition' /> 
										<!-- SCER 2644 Changes -->
										<entry key='sorterNumber' value='01' />
										<!--TGSR-427-->
										<entry key='displayBlankInEIPSWhenAmountZero' value='false' />	

									</map>
									<!-- Sequences Configuration AT GROUP Level -->
									<node name='sequences'>
										<node name='ItemDrnSequence'>
											<map>
												<entry key='initialValue' value='1' />
												<entry key='maximumValue' value='9223372036854775806' />
												<entry key='incrementStep' value='1' />
												<entry key='rollOver' value='true' />
												<entry key='hardReset' value='9223372036854775807' />
												<entry key='resetTo' value='1' />
												<entry key='resetDRNDaily' value='true' />
												<entry key='numberOfValues' value='500' />
											</map>
										</node>
									</node>
								</node>
								<node name='rdbLDCARTmt'> <!-- Group Name used for LargeDeposit if set to true -->
									<map>
										<entry key='description' value='rdbLD CART Mountain' />
										<entry key='priority' value='1' /><!--Priority in eips output file Name -->
										<entry key='stationNo' value='70' />
										<!-- Supported TM WorkType Examples for Commercial :111, 112, 113, 114, 132, 811, 131, 133, 834, 134 -->
										<entry key='pset' value='813' />
										<!-- Configuring what fields are used to define a unique batch 
											key -->
										<!-- For ex: <entry key='batchKey' value='User2+User3' /> -->
										<!-- For ex: <entry key='batchKey' value='SourceId' /> -->
										<entry key='batchKey' value='User1+User2+User3' />
										<entry key='exportPath' value='\\$1' />										
										<entry key='documentsGroup' value='defaultDocumentsGroup' />
										<entry key='holdoverDateSwitchTimeSchedule' value='default' />
										<entry key='generateDrn' value='true' />
										<entry key='site' value='site1' /> 			
										<entry key='region' value='region1' />
										<entry key='currencyCodeFace' value='CAD' />
										<entry key='batchMaxItemCount' value='3000' /> <!-- number of items -->
										<entry key='batchMaxValue' value='150000' />
										
										<!-- PSTC-2880 -->
										<entry key='itemTypeGroup' value='defaultItemTypeDefinition' /> 
										<!-- SCER 2644 Changes -->
										<entry key='sorterNumber' value='01' />
										<!--TGSR-427-->
										<entry key='displayBlankInEIPSWhenAmountZero' value='false' />	

									</map>
									<!-- Sequences Configuration AT GROUP Level -->
									<node name='sequences'>
										<node name='ItemDrnSequence'>
											<map>
												<entry key='initialValue' value='1' />
												<entry key='maximumValue' value='9223372036854775806' />
												<entry key='incrementStep' value='1' />
												<entry key='rollOver' value='true' />
												<entry key='hardReset' value='9223372036854775807' />
												<entry key='resetTo' value='1' />
												<entry key='resetDRNDaily' value='true' />
												<entry key='numberOfValues' value='500' />
											</map>
										</node>
									</node>
								</node>
								<node name='rdbLDCARTar'> <!-- Group Name used for LargeDeposit if set to true -->
									<map>
										<entry key='description' value='rdbLD CART Pacific' />
										<entry key='priority' value='1' /><!--Priority in eips output file Name -->
										<entry key='stationNo' value='72' />
										<!-- Supported TM WorkType Examples for Commercial :111, 112, 113, 114, 132, 811, 131, 133, 834, 134 -->
										<entry key='pset' value='814' />
										<!-- Configuring what fields are used to define a unique batch 
											key -->
										<!-- For ex: <entry key='batchKey' value='User2+User3' /> -->
										<!-- For ex: <entry key='batchKey' value='SourceId' /> -->
										<entry key='batchKey' value='User1+User2+User3' />
										<entry key='exportPath' value='\\$1' />										
										<entry key='documentsGroup' value='defaultDocumentsGroup' />
										<entry key='holdoverDateSwitchTimeSchedule' value='default' />
										<entry key='generateDrn' value='true' />
										<entry key='site' value='site1' /> 			
										<entry key='region' value='region1' />
										<entry key='currencyCodeFace' value='CAD' />
								    	<entry key='batchMaxItemCount' value='3000' /> <!-- number of items -->
										<entry key='batchMaxValue' value='150000' />
										
										<!-- PSTC-2880 -->
										<entry key='itemTypeGroup' value='defaultItemTypeDefinition' /> 
										<!-- SCER 2644 Changes -->
										<entry key='sorterNumber' value='01' />
										<!--TGSR-427-->
										<entry key='displayBlankInEIPSWhenAmountZero' value='false' />	

									</map>
									<!-- Sequences Configuration AT GROUP Level -->
									<node name='sequences'>
										<node name='ItemDrnSequence'>
											<map>
												<entry key='initialValue' value='1' />
												<entry key='maximumValue' value='9223372036854775806' />
												<entry key='incrementStep' value='1' />
												<entry key='rollOver' value='true' />
												<entry key='hardReset' value='9223372036854775807' />
												<entry key='resetTo' value='1' />
												<entry key='resetDRNDaily' value='true' />
												<entry key='numberOfValues' value='500' />
											</map>
										</node>
									</node>
								</node>
								<node name='rdbCARTpt'> <!-- Group Name used for LargeDeposit if set to true -->
									<map>
										<entry key='description' value='RDB CART Pacific' />
										<entry key='priority' value='1' /><!--Priority in eips output file Name -->
										<entry key='stationNo' value='50' />
										<!-- Supported TM WorkType Examples for Commercial :111, 112, 113, 114, 132, 811, 131, 133, 834, 134 -->
										<entry key='pset' value='114' />
										<!-- Configuring what fields are used to define a unique batch 
											key -->
										<!-- For ex: <entry key='batchKey' value='User2+User3' /> -->
										<!-- For ex: <entry key='batchKey' value='SourceId' /> -->
										<entry key='batchKey' value='User1+User2+User3' />
										<entry key='exportPath' value='\\$1' />										
										<entry key='documentsGroup' value='defaultDocumentsGroup' />
										<entry key='holdoverDateSwitchTimeSchedule' value='default' />
										<entry key='generateDrn' value='true' />
										<entry key='site' value='site1' /> 			
										<entry key='region' value='region1' />
										<entry key='currencyCodeFace' value='CAD' />
										<entry key='batchMaxItemCount' value='3000' /> <!-- number of items -->
										<entry key='batchMaxValue' value='150000' />
										
										<!-- PSTC-2880 -->
										<entry key='itemTypeGroup' value='defaultItemTypeDefinition' /> 
										<!-- SCER 2644 Changes -->
										<entry key='sorterNumber' value='01' />
										<!--TGSR-427-->
										<entry key='displayBlankInEIPSWhenAmountZero' value='false' />	

									</map>
									<!-- Sequences Configuration AT GROUP Level -->
									<node name='sequences'>
										<node name='ItemDrnSequence'>
											<map>
												<entry key='initialValue' value='1' />
												<entry key='maximumValue' value='9223372036854775806' />
												<entry key='incrementStep' value='1' />
												<entry key='rollOver' value='true' />
												<entry key='hardReset' value='9223372036854775807' />
												<entry key='resetTo' value='1' />
												<entry key='resetDRNDaily' value='true' />
												<entry key='numberOfValues' value='500' />
											</map>
										</node>
									</node>
								</node>
							</node>				
							
						</node>
						
						
						<node name='Teller'>
						<entry key='BranchNumber' value='9999' />
						<entry key='priority' value='1' /><!--Priority in eips output file Name -->
							<map>
								<entry key='configKey' value='SourceId' />
								<entry key='holdoverDateSwitchTimeSchedule' value='default' />
								<!-- examples <entry key='configKey' value='SourceLocation+SourceId'/> 
									<entry key='configKey' value='SourceLocation+SourceId+ACH.CustomerId+ACH.StandardEntryClassCode'/> 
									<entry key='configKey' value='TransactionSource+SourceId+LargeDeposit'/> 
									<entry key='configKey' value='SourceLocation+Branch+SourceId'/> -->
							</map>
							<node name='groupMapping'>
								<map>
									<!-- KEY names are configKey pattern values and these values can 
										also have wildcards, where '*' is for none or any string and '?' is for single 
										character -->
									<entry key='GRPTeller*' value='TellerGroup1' />
								</map>
							</node>

							<node name='groups'>
								<node name='TellerGroup1'> <!-- Group Name -->
									<map>
										<entry key='description' value='Teller Group1 Description' />
										<entry key='priority' value='1' /><!--Priority in eips output file Name -->
										<entry key='stationNo' value='4999' />
										<!-- Supported TM WorkType Examples for Teller :114, 814, 913, 713 -->
										<entry key='pset' value='114' />
										<!-- Configuring what fields are used to define a unique batch 
											key -->
										<!-- For ex: <entry key='batchKey' value='User2+User3' /> -->
										<!-- For ex: <entry key='batchKey' value='SourceId' /> -->
										<entry key='batchKey' value='TransactionSource+SourceId' />
										<entry key='exportPath' value='\\$1' />
										<entry key='customField1' value='10' />
										<entry key='customField2' value='435245' />
										<entry key='customField3' value='100' />
										<entry key='customField4' value='300' />
										<entry key='customField5' value='55555' />
										<entry key='documentsGroup' value='defaultDocumentsGroup' />
										<entry key='holdoverDateSwitchTimeSchedule' value='default' />
										<entry key='generateDrn' value='true' />
										<entry key='site' value='site1' /> 			
										<entry key='region' value='region1' />	
										<entry key='currencyCodeFace' value='CAD' />	
										<entry key='batchMaxItemCount' value='3000' /> <!-- number of items -->
										<entry key='batchMaxValue' value='150000' />
										
										<!-- PSTC-2880 -->
										<entry key='itemTypeGroup' value='defaultItemTypeDefinition' /> 
										<!-- SCER 2644 Changes -->
										<entry key='sorterNumber' value='01' />
										
															<!-- PSTC-1918 -->
										<entry key='separateBatchPerDebitCreditItems' value='true' />
										<!--TGSR-427-->
										<entry key='displayBlankInEIPSWhenAmountZero' value='false' />	
											 

									</map>

									<!-- Sequences Configuration AT GROUP Level -->
									<node name='sequences'>
										<node name='ItemDrnSequence'>
											<map>
												<entry key='initialValue' value='1' />
												<entry key='maximumValue' value='9223372036854775806' />
												<entry key='incrementStep' value='1' />
												<entry key='rollOver' value='true' />
												<entry key='hardReset' value='9223372036854775807' />
												<entry key='resetTo' value='1' />
												<entry key='resetDRNDaily' value='true' />
												<entry key='numberOfValues' value='500' />
											</map>
										</node>
									</node>
								</node>
							</node>
							
							<!-- Sequences Configuration AT SOURCETYPE Level -->
							<node name='sequences'>
								<node name='ItemDrnSequence'>
									<map>
										<entry key='initialValue' value='1' />
										<entry key='maximumValue' value='9223372036854775806' />
										<entry key='incrementStep' value='1' />
										<entry key='rollOver' value='true' />
										<entry key='hardReset' value='9223372036854775807' />
										<entry key='resetTo' value='1' />
										<entry key='resetDRNDaily' value='true' />
										<entry key='numberOfValues' value='500' />
									</map>
								</node>
							</node>

						</node> <!-- source type Teller -->			
						
						
					<node name='x937'>
					
									<!-- DRN Configuration - START-->
				<!--This drn formatting configuration will be used when the generateDrnDefault is set to false and the generateDrn is either set to false or not set for a particular group.-->
				<node name='drnConfig'>
					<!-- # DRN format is "ttrrttyyyymmddssss" # - rr is 2 digit region code 
						# - yyyymmdd is for the cycle date # - tttt is 4 digit station number # - 
						ssss is 4 digit sequence number -->
					<entry key='drn'
						value='{stationNumber,xstring,%r0r2sl}{regionCode,xstring,%l0l2sl}{str1}{str2}' />
					<node name='drn-parts'>
						<entry key='str1'
							value='{stationNumber,xstring,%l0l2sl}{cycleDate,date,yyyyMMdd}' />
						<entry key='str2' value='{nextDrnSequenceNumber,number,0000}' />
					</node>
				</node>
				
				<!-- This drn formatting configuration will be used when the generateDrnDefault is set to false and the generateDrn is set to true for a particular group.-->
				<node name='tcDrnConfig'>
					<!-- # DRN format is "ttrrttyyyymmddssss" # - rr is 2 digit region code 
						# - yyyymmdd is for the cycle date # - tttt is 4 digit station number # - 
						ssss is 4 digit sequence number -->
					<entry key='drn'
						value='{stationNumber,xstring,%r0r2sl}{regionCode,xstring,%l0l2sl}{str1}{str2}' />
					<node name='drn-parts'>
						<entry key='str1'
							value='{stationNumber,xstring,%l0l2sl}{cycleDate,date,yyyyMMdd}' />
						<entry key='str2' value='{nextDrnSequenceNumber,number,0000}' />
					</node>
				</node>
				<!--This config node will be used to format drn (for all the groups) when the generateDrnDefault is set to true.-->
				<!--Only If the generateDrnDefault is set to false,then this drnformat config will be used only for those groupswhose generatedrn is set to true.-->
				<node name='tcDrnFormat'>
					<!-- # DRN format is "ttrrttyyyymmddssss" # - rr is 2 digit region code 
						# - yyyymmdd is for the cycle date # - tttt is 4 digit station number # - 
						ssss is 4 digit sequence number -->
					<entry key='drn'
						value='{stationNumber,xstring,%r0r2sl}{regionCode,xstring,%l0l2sl}{str1}{str2}' />
					<node name='drn-parts'>
						<entry key='str1' value='00' />
						<entry key='str2' value='{nextDrnSequenceNumber,number,000000}' />
					</node>
				</node>
								
				
				<!-- DRN Configuration - END -->
						<entry key='BranchNumber' value='9999' />
						<entry key='priority' value='1' /><!--Priority in eips output file Name -->
							<map>
								<entry key='holdoverDateSwitchTimeSchedule' value='default' />		
								<entry key='configKey' value='immediateOriginRoutingNumber+fileIdModifier' />
							</map>
							<node name='groupMapping'>						
								<map>
									<entry key='324377011+A'  value='GRName1' /> <!-- value is group index -->
									<entry key='222222226'  value='GRName2' />
									<entry key='100000000'  value='GRName3' />
									<entry key='*' value='GRName4' />
								</map>
							</node>

							<node name='groups'>
								<node name='GRName1'> <!-- Group Name -->
									<map>
										<entry key='description' value='X937 GRName1 Description' />
										<entry key='priority' value='1' /><!--Priority in eips output file Name -->
										<entry key='stationNo' value='3999' />
										<!-- Supported TM WorkType Examples for Teller :114, 814, 913, 713 -->
										<entry key='pset' value='924' />
										<!-- Configuring what fields are used to define a unique batch 
											key -->
										<!-- For ex: <entry key='batchKey' value='User2+User3' /> -->
										<!-- For ex: <entry key='batchKey' value='SourceId' /> -->
										<entry key='batchKey' value='immediateOriginRoutingNumber+fileIdModifier' />
										<entry key='exportPath' value='\\$1' />
										<entry key='customField1' value='10' />
										<entry key='customField2' value='435245' />
										<entry key='customField3' value='100' />
										<entry key='customField4' value='300' />
										<entry key='customField5' value='55555' />
										<entry key='documentsGroup' value='x9DocumentsGroup' />
										<entry key='holdoverDateSwitchTimeSchedule' value='default' />
										<entry key='generateDrn' value='true' />
										<entry key='site' value='site1' /> 			
										<entry key='region' value='region1' />	
										<entry key='currencyCodeFace' value='CAD' />	
										<entry key='batchMaxItemCount' value='3000' /> <!-- number of items -->
										<entry key='batchMaxValue' value='150000' />
										<entry key='sorterNumber' value='01' />
										<!--TGSR-427-->
										<entry key='displayBlankInEIPSWhenAmountZero' value='false' />	
																				
									</map>

									<!-- Sequences Configuration AT GROUP Level -->
									<node name='sequences'>
										<node name='ItemDrnSequence'>
											<map>
												<entry key='initialValue' value='1' />
												<entry key='maximumValue' value='9223372036854775806' />
												<entry key='incrementStep' value='1' />
												<entry key='rollOver' value='true' />
												<entry key='hardReset' value='9223372036854775807' />
												<entry key='resetTo' value='1' />
												<entry key='resetDRNDaily' value='true' />
												<entry key='numberOfValues' value='500' />
											</map>
										</node>
									</node>
								</node>
								
							<node name='GRName2'> <!-- Group Name -->
									<map>
										<entry key='description' value='X937 GRName2 Description' />
										<entry key='priority' value='1' /><!--Priority in eips output file Name -->
										<entry key='stationNo' value='5999' />
										<!-- Supported TM WorkType Examples for Teller :114, 814, 913, 713 -->
										<entry key='pset' value='924' />
										<!-- Configuring what fields are used to define a unique batch 
											key -->
										<!-- For ex: <entry key='batchKey' value='User2+User3' /> -->
										<!-- For ex: <entry key='batchKey' value='SourceId' /> -->
										<entry key='batchKey' value='immediateOriginRoutingNumber+fileIdModifier' />
										<entry key='exportPath' value='\\$1' />
										<entry key='customField1' value='10' />
										<entry key='customField2' value='435245' />
										<entry key='customField3' value='100' />
										<entry key='customField4' value='300' />
										<entry key='customField5' value='55555' />
										<entry key='documentsGroup' value='x9DocumentsGroup' />
										<entry key='holdoverDateSwitchTimeSchedule' value='default' />
										<entry key='generateDrn' value='true' />
										<entry key='site' value='site1' /> 			
										<entry key='region' value='region1' />	
										<entry key='currencyCodeFace' value='CAD' />	
										<entry key='batchMaxItemCount' value='3000' /> <!-- number of items -->
										<entry key='batchMaxValue' value='150000' />
										<entry key='sorterNumber' value='01' />
										<!--TGSR-427-->
										<entry key='displayBlankInEIPSWhenAmountZero' value='false' />	
									</map>

									<!-- Sequences Configuration AT GROUP Level -->
									<node name='sequences'>
										<node name='ItemDrnSequence'>
											<map>
												<entry key='initialValue' value='1' />
												<entry key='maximumValue' value='9223372036854775806' />
												<entry key='incrementStep' value='1' />
												<entry key='rollOver' value='true' />
												<entry key='hardReset' value='9223372036854775807' />
												<entry key='resetTo' value='1' />
												<entry key='resetDRNDaily' value='true' />
												<entry key='numberOfValues' value='500' />
											</map>
										</node>
									</node>
								</node>
								
								
								
								<node name='GRName3'> <!-- Group Name -->
									<map>
										<entry key='description' value='X937 GRName3 Description' />
										<entry key='priority' value='1' /><!--Priority in eips output file Name -->
										<entry key='stationNo' value='6999' />
										<!-- Supported TM WorkType Examples for Teller :114, 814, 913, 713 -->
										<entry key='pset' value='924' />
										<!-- Configuring what fields are used to define a unique batch 
											key -->
										<!-- For ex: <entry key='batchKey' value='User2+User3' /> -->
										<!-- For ex: <entry key='batchKey' value='SourceId' /> -->
										<entry key='batchKey' value='immediateOriginRoutingNumber+fileIdModifier' />
										<entry key='exportPath' value='\\$1' />
										<entry key='customField1' value='10' />
										<entry key='customField2' value='435245' />
										<entry key='customField3' value='100' />
										<entry key='customField4' value='300' />
										<entry key='customField5' value='55555' />
										<entry key='documentsGroup' value='x9DocumentsGroup' />
										<entry key='holdoverDateSwitchTimeSchedule' value='default' />
										<entry key='generateDrn' value='true' />
										<entry key='site' value='site1' /> 			
										<entry key='region' value='region1' />	
										<entry key='currencyCodeFace' value='CAD' />	
										<entry key='batchMaxItemCount' value='3000' /> <!-- number of items -->
										<entry key='batchMaxValue' value='150000' />
										<entry key='sorterNumber' value='01' />
										<!--TGSR-427-->
										<entry key='displayBlankInEIPSWhenAmountZero' value='false' />	
									</map>

									<!-- Sequences Configuration AT GROUP Level -->
									<node name='sequences'>
										<node name='ItemDrnSequence'>
											<map>
												<entry key='initialValue' value='1' />
												<entry key='maximumValue' value='9223372036854775806' />
												<entry key='incrementStep' value='1' />
												<entry key='rollOver' value='true' />
												<entry key='hardReset' value='9223372036854775807' />
												<entry key='resetTo' value='1' />
												<entry key='resetDRNDaily' value='true' />
												<entry key='numberOfValues' value='500' />
											</map>
										</node>
									</node>
								</node>
								
								
								<node name='GRName4'> <!-- Group Name -->
									<map>
										<entry key='description' value='X937 GRName4 Description' />
										<entry key='priority' value='1' /><!--Priority in eips output file Name -->
										<entry key='stationNo' value='7999' />
										<!-- Supported TM WorkType Examples for Teller :114, 814, 913, 713 -->
										<entry key='pset' value='924' />
										<!-- Configuring what fields are used to define a unique batch 
											key -->
										<!-- For ex: <entry key='batchKey' value='User2+User3' /> -->
										<!-- For ex: <entry key='batchKey' value='SourceId' /> -->
										<entry key='batchKey' value='immediateOriginRoutingNumber+fileIdModifier' />
										<entry key='exportPath' value='\\$1' />
										<entry key='customField1' value='10' />
										<entry key='customField2' value='435245' />
										<entry key='customField3' value='100' />
										<entry key='customField4' value='300' />
										<entry key='customField5' value='55555' />
										<entry key='documentsGroup' value='x9DocumentsGroup' />
										<entry key='holdoverDateSwitchTimeSchedule' value='default' />
										<entry key='generateDrn' value='true' />
										<entry key='site' value='site1' /> 			
										<entry key='region' value='region1' />	
										<entry key='currencyCodeFace' value='CAD' />	
										<entry key='batchMaxItemCount' value='3000' /> <!-- number of items -->
										<entry key='batchMaxValue' value='150000' />
										<entry key='sorterNumber' value='01' />
										<!--TGSR-427-->
										<entry key='displayBlankInEIPSWhenAmountZero' value='false' />	
									</map>

									<!-- Sequences Configuration AT GROUP Level -->
									<node name='sequences'>
										<node name='ItemDrnSequence'>
											<map>
												<entry key='initialValue' value='1' />
												<entry key='maximumValue' value='9223372036854775806' />
												<entry key='incrementStep' value='1' />
												<entry key='rollOver' value='true' />
												<entry key='hardReset' value='9223372036854775807' />
												<entry key='resetTo' value='1' />
												<entry key='resetDRNDaily' value='true' />
												<entry key='numberOfValues' value='500' />
											</map>
										</node>
									</node>
								</node>
								
							</node>
							
							<!-- Sequences Configuration AT SOURCETYPE Level -->
							<node name='sequences'>
								<node name='ItemDrnSequence'>
									<map>
										<entry key='initialValue' value='1' />
										<entry key='maximumValue' value='9223372036854775806' />
										<entry key='incrementStep' value='1' />
										<entry key='rollOver' value='true' />
										<entry key='hardReset' value='9223372036854775807' />
										<entry key='resetTo' value='1' />
										<entry key='resetDRNDaily' value='true' />
										<entry key='numberOfValues' value='500' />
									</map>
								</node>
							</node>

						</node> <!-- X937 source type  -->					
						
					</node> <!-- source Types -->
					
				</node> <!-- group definition -->				
				
				<node name='groupChannelMapping'>
							<map>
								<entry key='AIT' value='PT' />
								<entry key='Commercial-Mobile' value='rdbEas' />
								<entry key='Commercial-OCD' value='' />
							</map>
				</node> <!-- group channel mappings -->	
			
				<!-- PSTC-2880 Itemtype configuration -->
				<node name='itemTypeDefinition'>
					<node name='defaultItemTypeDefinition'>
						<map>
							<entry key='0' value='cash-in' />
							<entry key='1' value='government' />
							<entry key='2' value='ON-US' />
							<entry key='3' value='other' />
							<entry key='5' value='questionable' />
							<entry key='8' value='rejected' />
							<entry key='97' value='deposit-slip' />
							<entry key='99' value='cash-out' />
						</map>
						
						<node name='itemTypeImageNotRequired'>
							<map>
								<entry key='1' value='false' />
								<entry key='2' value='false' />
								<entry key='3' value='false' />
								<entry key='5' value='false' />
								<entry key='8' value='false' />
								<entry key='0' value='true' />
								<entry key='9' value='true' />
								<entry key='97' value='false' />
								<entry key='99' value='true' />
							</map>
						</node>
				
						<node name='itemTypeMicrRequired'>
							<map>
								<entry key='0' value='false' />
								<entry key='1' value='true' />
								<entry key='2' value='true' />
								<entry key='3' value='true' />
								<entry key='5' value='true' />
								<entry key='8' value='true' />
								<entry key='97' value='false' />
								<entry key='99' value='false' />
							</map>
						</node>
						
						<node name='codelineConfigs'>
							<node name='cash-in'>
								<map>
									<entry key='codeline' value='                  d612122004d                           '/>
									<entry key='logicalPocketNumber' value='8' />
									<entry key='frontImage' value='/images/cashInFront.bmp' />
									<entry key='rearImage' value='/images/cashInRear.bmp' />
									<entry key='documentName' value='cash-in' />
									<entry key='ImageEndorsementFormats' value='documentName,amount,CodeLine' />
								</map>
								<node name='Fields'>
									<map>
										<entry key='amount' value='{item.itemAmount,string}' />
									</map>
								</node>
							</node>
							<node name='cash-out'>
								<map>
									<entry key='codeline' value='                  d612222001d     c      96            '/>
									<entry key='logicalPocketNumber' value='8' />
									<entry key='frontImage' value='/images/cashOutFront.bmp' />
									<entry key='rearImage' value='/images/cashOutRear.bmp' />
									<entry key='documentName' value='cash-out' />
									<entry key='ImageEndorsementFormats' value='documentName,amount,CodeLine' />
								</map>
								<node name='Fields'>
									<map>
										<entry key='amount' value='{item.itemAmount,string}' />
									</map>
								</node>
							</node>
							<node name='deposit-slip'>
								<map>
										<entry key='codeline' 
										 value='                  d161000017d     c      96            '/>
									<entry key='logicalPocketNumber' value='8' />
									<entry key='documentName' value='deposit-slip' />
								</map>
								<node name='Fields'>
									<map>
										<entry key='amount' value='{item.itemAmount,string}' />
									</map>
								</node>
							</node>
							
							<node name='default'>
								<map>
									<entry key='logicalPocketNumber' value='8' />
								</map>
								<node name='Fields'>
									<map>
										<entry key='amount' value='{item.itemAmount,string}' />
									</map>
								</node>
							</node>
						</node> <!-- codelineConfigs -->
					</node>

					<!-- ItemType defination for PT Group -->
					<node name='PTItemTypeDefinition'>
						<map>
							<entry key='0' value='cash-in' />
							<entry key='1' value='government' />
							<entry key='2' value='ON-US' />
							<entry key='3' value='other' />
							<entry key='5' value='questionable' />
							<entry key='8' value='rejected' />
							<entry key='97' value='deposit-slip' />
							<entry key='99' value='cash-out' />
						</map>
						
						<node name='itemTypeImageNotRequired'>
							<map>
								<entry key='1' value='false' />
								<entry key='2' value='false' />
								<entry key='3' value='false' />
								<entry key='5' value='false' />
								<entry key='8' value='false' />
								<entry key='0' value='true' />
								<entry key='9' value='true' />
								<entry key='97' value='true' />
								<entry key='99' value='true' />
							</map>
						</node>
			
						<!-- item types for whom MICR tag is required. -->
						<node name='itemTypeMicrRequired'>
							<map>
								<entry key='0' value='false' />
								<entry key='1' value='false' />
								<entry key='2' value='true' />
								<entry key='3' value='true' />
								<entry key='5' value='true' />
								<entry key='8' value='true' />
								<entry key='97' value='false' />
								<entry key='99' value='false' />
							</map>
						</node>
					
						<node name='codelineConfigs'>
							<node name='cash-in'>
								<map>
									<entry key='codeline' value='                  d612122004d                           '/>
									<entry key='logicalPocketNumber' value='8' />
									<entry key='frontImage' value='/images/cashInFront.bmp' />
									<entry key='rearImage' value='/images/cashInRear.bmp' />
									<entry key='documentName' value='cash-in' />
									<entry key='ImageEndorsementFormats' value='documentName,amount,CodeLine' />
								</map>
								<node name='Fields'>
									<map>
										<entry key='amount' value='{item.itemAmount,string}' />
									</map>
								</node>
							</node>
							<node name='cash-out'>
								<map>
									<entry key='codeline' value='                  d612222001d     c      96            '/>
									<entry key='logicalPocketNumber' value='8' />
									<entry key='frontImage' value='/images/cashOutFront.bmp' />
									<entry key='rearImage' value='/images/cashOutRear.bmp' />
									<entry key='documentName' value='cash-in' />
									<entry key='ImageEndorsementFormats' value='documentName,amount,CodeLine' />
								</map>
								<node name='Fields'>
									<map>
										<entry key='amount' value='{item.itemAmount,string}' />
									</map>
								</node>
							</node>
							<node name='deposit-slip'>
								<map>
										<entry key='codeline' 
										 value='                  d161000017d     c      96            '/>
									<entry key='logicalPocketNumber' value='8' />
									<entry key='documentName' value='deposit-slip' />
								</map>
								<node name='Fields'>
									<map>
										<entry key='amount' value='{item.itemAmount,string}' />
									</map>
								</node>
							</node>
							
							<node name='default'>
								<map>
									<entry key='logicalPocketNumber' value='8' />
								</map>
								<node name='Fields'>
									<map>
										<entry key='amount' value='{item.itemAmount,string}' />
									</map>
								</node>
							</node>
						</node> 
					</node>
				</node>

				<!-- PSTC-2880   Itemtype configuration -->
					
			<!-- Ghost Item Configuration -->
			
				<node name='documentGroups'>
					<node name='defaultDocumentsGroup'>
						<node name='run'>
							<node name='headerGhostDocuments'>
								<entry key='numberOfDocumentsConfig' value='1' />
								<node name='1'>
									<map>
										<entry key='codeline'
											 value="  c00004986c    d6666-6666d                               "  />
										<entry key='totalNumberOfDocs' value='1' />
										<entry key='logicalPocketNumber' value='1' />
										<entry key='documentTypeNumber' value='1' />
										<entry key='documentName' value='Electronic Image' />
										<entry key='frontImage' value='/images/trayHeaderFront.bmp' />
										<entry key='rearImage' value='/images/trayHeaderRear.bmp' />
										<entry key='ImageEndorsementFormats' value='documentName,amount,CodeLine' />
									</map>
									<node name='codeline-parts'>
										<map>
											<entry key='StationNumber' value='3999' />
										</map>
									</node>
								</node>
								<node name='2'>
									<map>
										<entry key='codeline'
											value= "  c0000{StationNumber}c    d6611-6611d                                " />
										<entry key='logicalPocketNumber' value='3' />
										<entry key='totalNumberOfDocs' value='0' />
										<entry key='documentTypeNumber' value='1' />
										<entry key='documentName' value='Electronic Image' />
										<entry key='frontImage' value='/images/trayHeaderFront.bmp' />
										<entry key='rearImage' value='/images/trayHeaderRear.bmp' />
										<entry key='ImageEndorsementFormats' value='documentName,amount,CodeLine' />
									</map>
								<node name='codeline-parts'>
										<map>
											<entry key='StationNumber' value='3999' />
										</map>
									</node>
								</node>
								<node name='3'>
									<map>
									<entry key='codeline'
											 value='  c100{StationNumber}c    d3333-6666d                              '  />
										<entry key='logicalPocketNumber' value='8' />
										<entry key='totalNumberOfDocs' value='0' />
										<entry key='documentTypeNumber' value='99' />
										<entry key='documentName' value='Electronic Image' />
										<entry key='ImageEndorsementFormats' value='documentName,amount' />
									</map>
								</node>
								<node name='4'>
									<map>
										<entry key='codeline'
											value="  c00004986c    d6666-6666d                               " />
											<!-- 4986 is Block Number For DefaultDocuments Group -->      
										<entry key='logicalPocketNumber' value='8' />
										<entry key='totalNumberOfDocs' value='0' />
										<entry key='documentTypeNumber' value='1' />
										<entry key='documentName' value='Electronic Image' />
										<entry key='frontImage' value='/images/blockHeaderFront.bmp' />
										<entry key='rearImage' value='/images/blockHeaderRear.bmp' />
										<entry key='ImageEndorsementFormats' value='documentName,amount,CodeLine' />
									</map>
								</node>
							</node>
							<node name='trailerGhostDocuments'>
								<entry key='numberOfDocumentsConfig' value='0' />
								<node name='1'>
									<map>
										<entry key='codeline'
											value="  c000c    d6611-6611d                                " />
										<entry key='logicalPocketNumber' value='8' />
										<entry key='totalNumberOfDocs' value='0' />
										<entry key='documentTypeNumber' value='1' />
										<entry key='documentName' value='Electronic Image' />
										<entry key='frontImage' value='/images/trayHeaderFront.bmp' />
										<entry key='rearImage' value='/images/trayHeaderRear.bmp' />
										<entry key='ImageEndorsementFormats' value='documentName,amount,CodeLine' />
									</map>
								</node>
							</node>
						</node>


						<node name='batch'>
							<node name='headerGhostDocuments'>
								<entry key='numberOfDocumentsConfig' value='1' />
								<node name='1'>
									<map>
										<entry key='codeline'                             
											 value='    c05004371c d5959-9300d                             '/>
										<entry key='logicalPocketNumber' value='1' />
										<entry key='totalNumberOfDocs' value='1' />
										<entry key='documentTypeNumber' value='1' />
										<entry key='documentName' value='Electronic Image' />
										<entry key='frontImage' value='/images/batchHeaderFront.bmp' />
										<entry key='rearImage' value='/images/batchHeaderRear.bmp' />
										<entry key='ImageEndorsementFormats' value='documentName,amount,CodeLine' />
									</map>
								</node>
							</node>
							<node name='trailerGhostDocuments'>
								<entry key='numberOfDocumentsConfig' value='0' />
								<node name='1'>
									<map>
										<entry key='codeline'
											value="                 d042000314d     c       96            " />
										<entry key='logicalPocketNumber' value='8' />
										<entry key='totalNumberOfDocs' value='0' />
										<entry key='documentTypeNumber' value='1' />
										<entry key='documentName' value='Electronic Image' />
										<entry key='frontImage' value='/images/batchHeaderFront.bmp' />
										<entry key='rearImage' value='/images/batchHeaderRear.bmp' />
										<entry key='ImageEndorsementFormats' value='documentName,amount,CodeLine' />
									</map>
								</node>
							</node>
						</node>
						
						
							<!--
							You Can Use Lookup Values like mentined in the commented node below.The values will be picked up From defaultConfigValues-lookup.xml module CommonComponent
							
							
						<node name='transaction'>
							<node name='headerGhostDocuments'>
								<entry key='numberOfDocumentsConfig' value='1' />
								<node name='1'>
									<map>
										<entry key='codeline' value="c{serial}c   d{routing}d  22        "/>
										<entry key='frontImage' value='/images/creditFront.bmp' />
										<entry key='totalNumberOfDocs' value='1' />
										<entry key='logicalPocketNumber' value='8' />
										<entry key='documentTypeNumber' value='1' />
										<entry key='rearImage' value='/images/creditRear.bmp' />
										<entry key='ImageEndorsementFormats' value='documentName,amount,CodeLine' />
									</map>
									<node name='codeline-parts'>
										<map>
										    <entry key='serial'   value='{lookup(sourceLocationTable,static.ISOCode,txn.transactionSource),xstring,%r0r2sl}'/>
											<entry key='routing'
											value='{lookup(sourceLocationTable,static.RTCode,txn.transactionSource),xstring,%r0r1sl}-
												   {lookup(sourceLocationTable,static.RTCode,txn.transactionSource),xstring,%r0r1sl}'/>		
										</map>	
									</node>
								</node>
					    </node>
					 </node>
				-->
				
						<node name='transaction'>
							<node name='headerGhostDocuments'>
								<entry key='numberOfDocumentsConfig' value='1' />
								<node name='1'>
									<map>
										<entry key='codeline'
										value="                 d121000044d     c       96            " />
										<!-- Example for transit# dynamic properties
										value="                 {transrouting}     c       96            " /> -->
										<entry key='frontImage' value='/images/creditFront.bmp' />
										<entry key='totalNumberOfDocs' value='1' />
										<entry key='logicalPocketNumber' value='8' />
										<entry key='documentName' value='TranHeader' />
										
										<entry key='documentTypeNumber' value='1' />
										<entry key='rearImage' value='/images/creditRear.bmp' />
										<entry key='ImageEndorsementFormats' value='documentName,amount,CodeLine' />
									</map>
									<!-- Example for transit# dynamic properties
									<node name='codeline-parts'>
										<map>
											<entry key='transrouting' value='{txn.RoutingNumber,string}' />
										</map>
									</node>-->
								</node>
							</node>
							<node name='trailerGhostDocuments'>
								<entry key='numberOfDocumentsConfig' value='0' />
								<node name='1'>
									<map>
										<entry key='logicalPocketNumber' value='8' />
										<entry key='totalNumberOfDocs' value='0' />
										<entry key='documentTypeNumber' value='1' />
										<entry key='documentName' value='Tran Trailer' />
										<entry key='frontImage' value='/images/creditFront.bmp' />
										<entry key='rearImage' value='/images/creditRear.bmp' />
										<entry key='ImageEndorsementFormats' value='documentName,amount,CodeLine' />
										<entry key='codeline'
											value="c{serial}c   d{routing}d   c{account}  {PC}        " />
									</map>
									<node name='codeline-parts'>
										<map>
											<entry key='serial' value='123456' />
											<entry key='routing' value='9696-9996' />
											<entry key='account' value='32015078' />
											<entry key='PC' value='98' />
										</map>
									</node>
									<node name='Fields'>
										<map><!-- amount should be zero in case of branch flow-->
											<entry key='amount' value='{txn.depositAmount,string}' />
											<!-- <entry key='Field7' value='{txn.sequence,string}' /> <entry 
												key='Field9' value='{txn.depositRouting,string}' /> <entry key='Field10' 
												value='{txn.depositAccount,string}' /> -->
										</map>
									</node>
								</node>
							</node>
						</node>						
					</node>
					
					
					<node name='docGroup2'>
						<node name='run'>
							<node name='headerGhostDocuments'>
								<entry key='numberOfDocumentsConfig' value='4' />
								<node name='4'>
									<map>
										<entry key='codeline'
											value="  c100   d6611-6611d                               " />
										<entry key='totalNumberOfDocs' value='1' />
										<entry key='logicalPocketNumber' value='3' />
										<entry key='documentTypeNumber' value='1' />
										<entry key='documentName' value='Electronic Image' />
										<entry key='frontImage' value='/images/trayHeaderFront.bmp' />
										<entry key='rearImage' value='/images/trayHeaderRear.bmp' />
										<entry key='ImageEndorsementFormats' value='documentName,amount,CodeLine' />
									</map>
								</node>
								<node name='3'>
									<map>
										<entry key='codeline'
											value="  c100   d6611-6611d                               " />
										<entry key='logicalPocketNumber' value='8' />
										<entry key='totalNumberOfDocs' value='1' />
										<entry key='documentTypeNumber' value='1' />
										<entry key='documentName' value='Electronic Image' />
										<entry key='frontImage' value='/images/trayHeaderFront.bmp' />
										<entry key='rearImage' value='/images/trayHeaderRear.bmp' />
										<entry key='ImageEndorsementFormats' value='documentName,amount,CodeLine' />
									</map>
								</node>
								<node name='2'>
									<map>
										<entry key='codeline'
											value="  c100   d6611-6611d                               " />
										<entry key='logicalPocketNumber' value='8' />
										<entry key='totalNumberOfDocs' value='10' />
										<entry key='documentTypeNumber' value='4' />
										<entry key='documentName' value='Electronic Image' />
										<entry key='ImageEndorsementFormats' value='documentName,amount,CodeLine' />
									</map>
								</node>
								<node name='1'>
									<map>
										<entry key='codeline'
											value="  c00004986c    d6666-6666d                               " />
										<entry key='logicalPocketNumber' value='1' />
										<entry key='totalNumberOfDocs' value='1' />
										<entry key='documentTypeNumber' value='1' />
										<entry key='documentName' value='Electronic Image' />
										<entry key='frontImage' value='/images/blockHeaderFront.bmp' />
										<entry key='rearImage' value='/images/blockHeaderRear.bmp' />
										<entry key='ImageEndorsementFormats' value='documentName,amount,CodeLine' />
									</map>
								</node>
							</node>
							<node name='trailerGhostDocuments'>
								<entry key='numberOfDocumentsConfig' value='0' />
								<node name='1'>
									<map>
										<entry key='codeline'
											value="  c000c    d6611-6611d                                " />
										<entry key='logicalPocketNumber' value='8' />
										<entry key='totalNumberOfDocs' value='1' />
										<entry key='documentTypeNumber' value='1' />
										<entry key='documentName' value='Electronic Image' />
										<entry key='frontImage' value='/images/trayHeaderFront.bmp' />
										<entry key='rearImage' value='/images/trayHeaderRear.bmp' />
										<entry key='ImageEndorsementFormats' value='documentName,amount,CodeLine' />
									</map>
								</node>
							</node>
						</node>


						<node name='batch'>
							<node name='headerGhostDocuments'>
								<entry key='numberOfDocumentsConfig' value='1' />
								<node name='1'>
									<map>
										<entry key='codeline'
											value="c0599995555c   d7561-1756d   c111111111       96        " />
										<entry key='logicalPocketNumber' value='8' />
										<entry key='totalNumberOfDocs' value='1' />
										<entry key='documentTypeNumber' value='1' />
										<entry key='documentName' value='Electronic Image' />
										<entry key='frontImage' value='/images/batchHeaderFront.bmp' />
										<entry key='rearImage' value='/images/batchHeaderRear.bmp' />
										<entry key='ImageEndorsementFormats' value='documentName,amount,CodeLine' />
									</map>
								</node>
							</node>
							<node name='trailerGhostDocuments'>
								<entry key='numberOfDocumentsConfig' value='0' />
								<node name='1'>
									<map>
										<entry key='codeline'
											value="                 d042000314d     c                     " />
										<entry key='logicalPocketNumber' value='8' />
										<entry key='totalNumberOfDocs' value='1' />
										<entry key='documentTypeNumber' value='1' />
										<entry key='documentName' value='Electronic Image' />
										<entry key='frontImage' value='/images/batchHeaderFront.bmp' />
										<entry key='rearImage' value='/images/batchHeaderRear.bmp' />
										<entry key='ImageEndorsementFormats' value='documentName,amount,CodeLine' />
									</map>
								</node>
							</node>
						</node>
						<node name='transaction'>
							<node name='headerGhostDocuments'>
								<entry key='numberOfDocumentsConfig' value='1' />
								<node name='1'>
									<map>
										<entry key='codeline'
											value="                 d121000044d     c       96            " />
										<entry key='frontImage' value='/images/creditFront.bmp' />
										<entry key='totalNumberOfDocs' value='1' />
										<entry key='documentTypeNumber' value='1' />
										<entry key='documentName' value='Transaction Header' />
										<entry key='rearImage' value='/images/creditFront.bmp' />
										<entry key='rearImage' value='/images/creditRear.bmp' />
										<entry key='ImageEndorsementFormats' value='documentName,amount,CodeLine' />
									</map>
									<node name='codeline-parts'>
										<map>
											<entry key='serial' value='123456789' />
											<entry key='account' value='{txn.accountNumber,xstring,%l l14sl}' />
											<entry key='routing' value='1234-{txn.routingNumber,xstring,%r0r4sl}' />
											<entry key='PC' value='452' />
										</map>
									</node>
									<node name='Fields'>
										<map><!-- amount should be zero in case of branch flow-->
											<entry key='amount' value='0' />
											<!-- <entry key='Field7' value='{txn.sequence,string}' /> <entry 
												key='Field9' value='{txn.depositRouting,string}' /> <entry key='Field10' 
												value='{txn.depositAccount,string}' /> -->
										</map>
									</node>
								</node>
							</node>
							<node name='trailerGhostDocuments'>
								<entry key='numberOfDocumentsConfig' value='0' />
								<node name='1'>
									<map>
										<entry key='logicalPocketNumber' value='8' />
										<entry key='totalNumberOfDocs' value='1' />
										<entry key='documentTypeNumber' value='1' />
										<entry key='documentName' value='Electronic Image' />
										<entry key='frontImage' value='/images/creditFront.bmp' />
										<entry key='rearImage' value='/images/creditRear.bmp' />
										<entry key='ImageEndorsementFormats' value='documentName,amount,CodeLine' />
										<entry key='codeline'
											value="c{serial}c   d{routing}d   c{account}  {PC}        " />
									</map>
									<node name='codeline-parts'>
										<map>
											<entry key='serial' value='999999999' />
											<entry key='routing' value='9999-9999' />
											<entry key='account' value='99999' />
											<entry key='PC' value='99' />
										</map>
									</node>
									<node name='Fields'>
										<map><!--should be zero in case of branch flow-->
											<entry key='amount' value='0' />
											<!-- <entry key='Field7' value='{txn.sequence,string}' /> <entry 
												key='Field9' value='{txn.depositRouting,string}' /> <entry key='Field10' 
												value='{txn.depositAccount,string}' /> -->
										</map>
									</node>
								</node>
							</node>
						</node>						
					</node>		
					
										
					<node name='x9DocumentsGroup'>
						<node name='run'>
							<node name='headerGhostDocuments'>
								<entry key='numberOfDocumentsConfig' value='2' />
								<node name='1'>
									<map>
										<entry key='codeline'
											value="                d{routing}d              b{amount}b                  " />
										<entry key='logicalPocketNumber' value='1' />
										<entry key='totalNumberOfDocs' value='1' />
										<entry key='x9Item' value='P' />
										<entry key='documentTypeNumber' value='1' />
										<entry key='documentName' value='Physical Collection Header' />
										<entry key='frontImage' value='/images/blockHeaderFront.bmp' />
										<entry key='rearImage' value='/images/blockHeaderRear.bmp' />
										<entry key='ImageEndorsementFormats' value='documentName,amount,CodeLine' />
									</map>
									<node name='codeline-parts'>
										<map>
											<entry key='routing' value='6666-6666' />
											<entry key='amount' value='{amount,string}' />
										</map>
									</node>
								</node>
								<node name='2'>
									<map>
										<entry key='codeline'
											value="                d{routing}d              b{amount}b                  " />
										<entry key='logicalPocketNumber' value='1' />
										<entry key='totalNumberOfDocs' value='1' />
										<entry key='x9Item' value='V' />
										<entry key='documentTypeNumber' value='1' />
										<entry key='documentName' value='Virtual Collection Header' />
										<entry key='frontImage' value='/images/blockHeaderFront.bmp' />
										<entry key='rearImage' value='/images/blockHeaderRear.bmp' />
										<entry key='ImageEndorsementFormats' value='documentName,amount,CodeLine' />
									</map>
									<node name='codeline-parts'>
										<map>
											<entry key='routing' value='6666-6666' />
											<entry key='amount' value='{amount,string}' />
										</map>
									</node>
								</node>
							</node>
							<node name='trailerGhostDocuments'>
								<entry key='numberOfDocumentsConfig' value='0' />
								<node name='1'>
									<map>
										<entry key='codeline'
											value="  c000c    d6611-6611d                                " />
										<entry key='logicalPocketNumber' value='8' />
										<entry key='totalNumberOfDocs' value='1' />
										<entry key='x9Item' value='V' />
										<entry key='documentTypeNumber' value='1' />
										<entry key='documentName' value='Virtual Collection Trailer' />
										<entry key='frontImage' value='/images/blockTrailerFront.bmp' />
										<entry key='rearImage' value='/images/blockTrailerRear.bmp' />
										<entry key='ImageEndorsementFormats' value='documentName,amount,CodeLine' />
									</map>
								</node>
							</node>
						</node>


						<node name='batch'>
							<node name='headerGhostDocuments'>
								<entry key='numberOfDocumentsConfig' value='2' />
								<node name='1'>
									<map>
										<entry key='codeline'                             
											 value='    d{routing}d  c   {PC}   b{amount}b         '/>
										<entry key='logicalPocketNumber' value='1' />
										<entry key='totalNumberOfDocs' value='1' />
										<entry key='x9Item' value='P' />
										<entry key='documentTypeNumber' value='1' />
										<entry key='documentName' value='Physical Batch Header' />
										<entry key='frontImage' value='/images/batchHeaderFront.bmp' />
										<entry key='rearImage' value='/images/batchHeaderRear.bmp' />
										<entry key='ImageEndorsementFormats' value='documentName,amount,CodeLine' />
									</map>
									<node name='codeline-parts'>
										<map>
											<entry key='routing' value='5959-9300' />
											<entry key='PC' value='999' />
											<entry key='amount' value='{amount,string}' />
										</map>
									</node>
								</node>
								<node name='2'>
									<map>
										<entry key='codeline'                             
											 value='    d{routing}d  c   {PC}   b{amount}b         '/>
										<entry key='logicalPocketNumber' value='1' />
										<entry key='totalNumberOfDocs' value='1' />
										<entry key='x9Item' value='V' />
										<entry key='documentTypeNumber' value='1' />
										<entry key='documentName' value='Virtual Batch Header' />
										<entry key='frontImage' value='/images/batchHeaderFront.bmp' />
										<entry key='rearImage' value='/images/batchHeaderRear.bmp' />
										<entry key='ImageEndorsementFormats' value='documentName,amount,CodeLine' />
									</map>
									<node name='codeline-parts'>
										<map>
											<entry key='routing' value='5959-9300' />
											<entry key='PC' value='999' />
											<entry key='amount' value='{amount,string}' />
										</map>
									</node>
								</node>
							</node>
							<node name='trailerGhostDocuments'>
								<entry key='numberOfDocumentsConfig' value='0' />
								<node name='1'>
									<map>
										<entry key='codeline'
											value="                 d042000314d     c                     " />
										<entry key='logicalPocketNumber' value='8' />
										<entry key='totalNumberOfDocs' value='1' />
										<entry key='x9Item' value='V' />
										<entry key='documentTypeNumber' value='1' />
										<entry key='documentName' value='Virtual Batch Trailer' />
										<entry key='frontImage' value='/images/batchTrailerFront.bmp' />
										<entry key='rearImage' value='/images/batchTrailerRear.bmp' />
										<entry key='ImageEndorsementFormats' value='documentName,amount,CodeLine' />
									</map>
								</node>
							</node>
						</node>
						
						<node name='transaction'>
							<node name='headerGhostDocuments'>
								<entry key='numberOfDocumentsConfig' value='2' />
								<node name='1'>
									<map>
										<entry key='codeline'
											value="                 d121000044d     c       96            " />	
										<entry key='totalNumberOfDocs' value='1' />
										<entry key='x9Item' value='P' />
										<entry key='documentTypeNumber' value='1' />
										<entry key='documentName' value='Physical Transaction Header' />
										<entry key='frontImage' value='/images/creditFront.bmp' />
										<entry key='rearImage' value='/images/creditRear.bmp' />
										<entry key='ImageEndorsementFormats' value='documentName,amount,CodeLine' />
									</map>
								</node>
								<node name='2'>
									<map>
										<entry key='codeline'
											value="                 d121000044d     c       96            " />	
										<entry key='totalNumberOfDocs' value='1' />
										<entry key='x9Item' value='V' />
										<entry key='documentTypeNumber' value='1' />
										<entry key='documentName' value='Virtual Transaction Header' />
										<entry key='frontImage' value='/images/creditFront.bmp' />
										<entry key='rearImage' value='/images/creditRear.bmp' />
										<entry key='ImageEndorsementFormats' value='documentName,amount,CodeLine' />
									</map>
								</node>
							</node>
							<node name='trailerGhostDocuments'>
								<entry key='numberOfDocumentsConfig' value='0' />
								<node name='1'>
									<map>
										<entry key='logicalPocketNumber' value='8' />
										<entry key='totalNumberOfDocs' value='1' />
										<entry key='x9Item' value='V' />
										<entry key='documentTypeNumber' value='1' />
										<entry key='documentName' value='Virtual Transaction Trailer' />
										<entry key='frontImage' value='/images/creditFront.bmp' />
										<entry key='rearImage' value='/images/creditRear.bmp' />
										<entry key='ImageEndorsementFormats' value='documentName,amount,CodeLine' />
										<entry key='codeline'
											value="                d15895344d     c       88           " />
									</map>
								</node>
							</node>
						</node>						
					</node>	
					
					
					
			<node name='BranchDocumentsGroup'>
						<node name='run'>
							<node name='headerGhostDocuments'>
								<entry key='numberOfDocumentsConfig' value='1' />
								<node name='1'>
									<map>
										<entry key='codeline'
											value="                 d121000044d     c       96            " />
										<entry key='totalNumberOfDocs' value='1' />
										<entry key='logicalPocketNumber' value='8' />
										<entry key='documentTypeNumber' value='1' />
										<entry key='documentName' value='Run Header Image' />
										<entry key='frontImage' value='/images/blockHeaderFront.bmp' />
										<entry key='rearImage' value='/images/blockHeaderFront.bmp' />
										<entry key='ImageEndorsementFormats' value='documentName,amount,CodeLine' /> 
									</map>
								</node>
								<node name='2'>
									<map>
									<entry key='codeline'
											value="                 d121000045d     c       96            " />
										<entry key='logicalPocketNumber' value='3' />
										<entry key='totalNumberOfDocs' value='1' />
										<entry key='documentTypeNumber' value='1' />
										<entry key='documentName' value='Tray Header' />
										<entry key='frontImage' value='/images/trayHeaderFront.bmp' />
										<entry key='rearImage' value='/images/trayHeaderRear.bmp' />
										<entry key='ImageEndorsementFormats' value='documentName,amount,CodeLine' />
									</map>
								</node>
								<node name='3'>
									<map>
										<entry key='codeline'
											value="                 d121000046d     c       96            " />
										<entry key='logicalPocketNumber' value='8' />
										<entry key='totalNumberOfDocs' value='1' />
										<entry key='documentTypeNumber' value='99' />
									</map>
								</node>
				
							</node>
							<node name='trailerGhostDocuments'>
								<entry key='numberOfDocumentsConfig' value='0' />
								<node name='1'>
									<map>
										<entry key='codeline'
											value="  c000c    d6611-6611d                                " />
										<entry key='logicalPocketNumber' value='8' />
										<entry key='totalNumberOfDocs' value='1' />
										<entry key='documentTypeNumber' value='1' />
										<entry key='documentName' value='Tray Trailer' />
										<entry key='frontImage' value='/images/trayHeaderFront.bmp' />
										<entry key='rearImage' value='/images/trayHeaderRear.bmp' />
										<entry key='ImageEndorsementFormats' value='documentName,amount,CodeLine' />
									</map>
								</node>
							</node>
						</node>


						<node name='batch'>
							<node name='headerGhostDocuments'>
								<entry key='numberOfDocumentsConfig' value='1' />
								<node name='1'>
									<map>
										<entry key='codeline'
											value="c0599995555c   d7561-1756d   c111111111       96        " />
										<entry key='logicalPocketNumber' value='8' />
										<entry key='totalNumberOfDocs' value='1' />
										<entry key='documentTypeNumber' value='1' />
										<entry key='documentName' value='Batch Header' />
										<entry key='frontImage' value='/images/batchHeaderFront.bmp' />
										<entry key='rearImage' value='/images/batchHeaderRear.bmp' />
										<entry key='ImageEndorsementFormats' value='documentName,amount,CodeLine' /> 
									</map>
								</node>
							</node>
							<node name='trailerGhostDocuments'>
								<entry key='numberOfDocumentsConfig' value='0' />
								<node name='1'>
									<map>
										<entry key='codeline'
											value="                 d042000314d     c                     " />
										<entry key='logicalPocketNumber' value='8' />
										<entry key='totalNumberOfDocs' value='1' />
										<entry key='documentTypeNumber' value='1' />
										<entry key='documentName' value='Batch Trailer' />
										<entry key='frontImage' value='/images/batchHeaderFront.bmp' />
										<entry key='rearImage' value='/images/batchHeaderRear.bmp' />
										<entry key='ImageEndorsementFormats' value='documentName,amount,CodeLine' />
									</map>
								</node>
							</node>
						</node>
						<node name='transaction'>
							<node name='headerGhostDocuments'>
								<entry key='numberOfDocumentsConfig' value='1' />
								<node name='1'>
									<map>
										<entry key='codeline'
											value="                 d121000044d     c       96            " />
										<entry key='frontImage' value='/images/creditFront.bmp' />
										<entry key='totalNumberOfDocs' value='1' />
										<entry key='documentName' value='Ghost Deposit' />
										<entry key='documentTypeNumber' value='1' />
										<entry key='rearImage' value='/images/creditFront.bmp' />
										<entry key='rearImage' value='/images/creditRear.bmp' />
										<entry key='ImageEndorsementFormats' value='documentName,amount,CodeLine' />
									</map>
								</node>
							</node>
							<node name='trailerGhostDocuments'>
								<entry key='numberOfDocumentsConfig' value='0' />
								<node name='1'>
									<map>
										<entry key='logicalPocketNumber' value='8' />
										<entry key='totalNumberOfDocs' value='1' />
										<entry key='documentTypeNumber' value='1' />
										<entry key='documentName' value='Ghost Deposit Trailer' />
										<entry key='frontImage' value='/images/creditFront.bmp' />
										<entry key='rearImage' value='/images/creditRear.bmp' />
										<entry key='ImageEndorsementFormats' value='documentName,amount,CodeLine' />
										<entry key='codeline'
											value="c{serial}c   d{routing}d   c{account}  {PC}        " />
									</map>
									<node name='codeline-parts'>
										<map>
											<entry key='serial' value='999999999' />
											<entry key='routing' value='9999-9999' />
											<entry key='account' value='99999' />
											<entry key='PC' value='99' />
										</map>
									</node>
									<node name='Fields'>
										<map><!--should be zero in case of branch flow-->
											<entry key='amount' value='0' />
											<!-- <entry key='Field7' value='{txn.sequence,string}' /> <entry 
												key='Field9' value='{txn.depositRouting,string}' /> <entry key='Field10' 
												value='{txn.depositAccount,string}' /> -->
										</map>
									</node>
								</node>
							</node>
						</node>						
					</node>	
								
				</node>
				
				<node name='holdoverDateSwitchTimeSchedule'>
					<node name='default'>
						<map>
							<entry key='Sunday' value='' />
							<entry key='Monday' value='Sunday 09:00' />
							<entry key='Tuesday' value='Monday 23:00' />
							<entry key='Wednesday' value='Tuesday 23:00' />
							<entry key='Thursday' value='Wednesday 23:00' />
							<entry key='Friday' value='Thursday 23:00' />
							<entry key='Saturday' value='' />
						</map>
					</node>
					<node name='default1'>
						<map>
							<entry key='Sunday' value='' />
							<entry key='Monday' value='Sunday 09:00' />
							<entry key='Tuesday' value='Monday 09:00' />
							<entry key='Wednesday' value='Tuesday 09:00' />
							<entry key='Thursday' value='Wednesday 09:00' />
							<entry key='Friday' value='Thursday 09:00' />
							<entry key='Saturday' value='' />
						</map>
					</node>
				</node>
				
				<node name='cutOverTimePset'>
					<node name='Group1'> <!-- Group Name -->
						<node name='1'> <!-- working day index -->
							<map>
								<entry key='20:00:00' value='11' />
								<entry key='22:00:00' value='12' />
								<entry key='23:00:00' value='13' />
							</map>
						</node>
						<node name='2'>
							<map>
								<entry key='10:00:00' value='14' />
								<entry key='13:00:00' value='15' />
								<entry key='22:00:00' value='16' />
							</map>
						</node>
						<node name='3'>
							<map>
								<entry key='02:00:00' value='11' />
								<entry key='03:00:00' value='12' />
								<entry key='22:00:00' value='13' />
							</map>
						</node>
						<node name='4'>
							<map>
								<entry key='02:00:00' value='11' />
								<entry key='10:00:00' value='12' />
								<entry key='22:00:00' value='13' />
							</map>
						</node>
						<node name='5'>
							<map>
								<entry key='02:00:00' value='14' />
								<entry key='20:00:00' value='15' />
								<entry key='22:00:00' value='16' />
							</map>
						</node>
						<node name='6'>
							<map>
								<entry key='02:00:00' value='11' />
								<entry key='12:00:00' value='12' />
								<entry key='22:00:00' value='13' />
							</map>
						</node>
						<node name='7'>
							<map>
								<entry key='02:00:00' value='11' />
								<entry key='15:00:00' value='12' />
								<entry key='22:00:00' value='13' />
							</map>
						</node>
					</node>
				</node>

				<node name='defaultListCutOverTimePset'>
					
						<node name='1'> <!-- working day index -->
							<map>
								<entry key='20:00:00' value='11' />
								<entry key='22:00:00' value='12' />
								<entry key='23:00:00' value='13' />
							</map>
						</node>
						<node name='2'>
							<map>
								<entry key='10:00:00' value='14' />
								<entry key='13:00:00' value='15' />
								<entry key='22:00:00' value='16' />
							</map>
						</node>
						<node name='3'>
							<map>
								<entry key='02:00:00' value='11' />
								<entry key='03:00:00' value='12' />
								<entry key='22:00:00' value='13' />
							</map>
						</node>
						<node name='4'>
							<map>
								<entry key='02:00:00' value='11' />
								<entry key='10:00:00' value='12' />
								<entry key='22:00:00' value='13' />
							</map>
						</node>
						<node name='5'>
							<map>
								<entry key='02:00:00' value='14' />
								<entry key='20:00:00' value='15' />
								<entry key='22:00:00' value='16' />
							</map>
						</node>
						<node name='6'>
							<map>
								<entry key='02:00:00' value='11' />
								<entry key='12:00:00' value='12' />
								<entry key='22:00:00' value='13' />
							</map>
						</node>
						<node name='7'>
							<map>
								<entry key='02:00:00' value='11' />
								<entry key='15:00:00' value='12' />
								<entry key='22:00:00' value='13' />
							</map>
						</node>
					
				</node>
				
			<node name='sequences'>
				<node name='BatchGhostDocSerialSeq'>
					<map>
						<entry key='initialValue' value='1' />
						<entry key='maximumValue' value='99999' />
						<entry key='incrementStep' value='1' />
						<entry key='rollOver' value='true' />
						<entry key='numberOfValues' value='500' />
					</map>
				</node>
			</node>	
			<node name='sequences'>
				<node name='BlockGhostDocSerialSeq'>
					<map>
						<entry key='initialValue' value='1' />
						<entry key='maximumValue' value='99999' />
						<entry key='incrementStep' value='1' />
						<entry key='rollOver' value='true' />
						<entry key='numberOfValues' value='500' />
					</map>
				</node>
			</node>
			
			<node name='sequences'>
				<node name='RunSequence'>
					<map>
						<entry key='initialValue' value='1' />
						<entry key='maximumValue' value='99' />
						<entry key='incrementStep' value='1' />
						<entry key='rollOver' value='true' />
						<entry key='numberOfValues' value='1' />
						<entry key='hardReset' value='100' />
						<entry key='resetTo' value='1' />
						<entry key='sequenceThreshold' value='1' />
						<entry key='resetDRNDaily' value='false' />
					</map>
				</node>
			</node>	
				<node name='sequences'>
				 <node name='EntryNumberSequence'>
					<map>
						<entry key='initialValue' value='1' />
						<entry key='maximumValue' value='9999' />
						<entry key='incrementStep' value='1' />
						<entry key='rollOver' value='true' />
						<entry key='numberOfValues' value='1' />
						<entry key='resetDRNDaily' value='true' />
					</map>
				</node>
			</node>	
			
				<node name='Locale'>
					<map>
						<entry key='localeString' value='en-US' />
						<entry key='divideByValue' value='100' />
						<!--      
                               devideByValue-The amount in checks' transactions is in lower denominations. Needs 
                                               to be divided by this value for display purpose.
                                             Set this to 10/100/1000 wherever applicable  -->
						
					</map>
			
			</node>	
				
		<node name='TCPurgeDB'>
				 <map>
					<entry key='retentionDays' value='30' />

				</map>
			</node>	
			
		<node name='WbiConfigNodes'>
				<node name='GroupDefaultWbiDepositNode'>
					<map>
						<!-- # Allows deposits from TC to be put into Aptra via Web-Banking 
							Interface -->
						
						<!-- # Properties for exported PutDepositRequest XML -->
						<entry key='bankName' value='Bank of Northfield' />
						<entry key='requestVersion' value='01.00.01' />
						<entry key='bankUserId' value='bank_admin_cm' />
						<entry key='bankUserPassword' value='d' />
						<entry key='bankDomain' value='BankDomain' />
						

						<!-- # Number of thread in the thread pool -->
						<entry key='threadPoolSize' value='10' />

						<!-- # Amount Method could be MICR, CAR/LAR, OCR, Keyed, Calculated, 
							Other -->
						<entry key='depositSlipAmountMethod' value='Keyed' />
						<entry key='checkAmountMethod' value='CAR/LAR' />

						<!-- # Codeline Method could be MICR, OCR, Other -->
						<entry key='depositSlipCodelineMethod' value='Other' />
						<entry key='checkCodelineMethod' value='MICR' />

						<!-- # Aptra webservice properties -->
						<entry key='endPointAddress'
							value='http://153.71.22.5:9080/webinterface/services/remoteservices' />
						<!-- # Incase Aptra service is unavailable how many times to retry -->
						<entry key='numberOfRetries' value='1' />
						<!-- # Incase Aptra service is unavailable the retry interval in seconds -->
						<entry key='retryInterval' value='5' />

						<!-- # Generate keys -> Deposit/Transaction ID and Item IDs and set 
							into WBI request XML (for PWE) as well as CDS XML (for TM) # enableAptraDataPerfection 
							= true # enableAptraDataPerfection = false -->
						<entry key='enableAptraDataPerfection' value='true' />

						<!-- # The Deposit ID from Aptra response needs to be set into Deposit 
							Slip codeline fields 8 or 9 or 10 # This property works only when setAptraResponseintoCDS 
							property is true # The valid values can be 8 or 9 or 10 only -->
						<entry key='aptraDepositIdToDepositSlipCodeline' value='8' />

						<!-- # If aptraCaptureDRNField is 0 then CS calculated Item Id is set 
							to captureDRN field # If aptraCaptureDRNField is 1 then ScannerSequenceNumber 
							of input XML is set to captureDRN field # Can be upgraded in future if more 
							options are to be given -->
						<entry key='aptraCaptureDRNField' value='0' />

						<!-- # List of severity codes in case of failure -->
						<entry key='severityCodesForFailure' value='FATAL,ERROR' />

						<!-- # List of error codes in case of failure -->
						<entry key='errorCodesForFailure' value='200,201,300,301' />
					</map>
				</node>
			</node>
			
		<node name='DeFaultWBIConfigNode'>
					<map>
						<entry key='putDeposit' value='true' />
						
						<!-- # Properties for exported PutDepositRequest XML -->
						<entry key='bankName' value='Bank of Northfield' />
						<entry key='requestVersion' value='01.00.01' />
						<entry key='bankUserId' value='bank_admin_cm' />
						<entry key='bankUserPassword' value='d' />
						<entry key='bankDomain' value='BankDomain' />
						

						<!-- # Number of thread in the thread pool -->
						<entry key='threadPoolSize' value='10' />

						<!-- # Amount Method could be MICR, CAR/LAR, OCR, Keyed, Calculated, 
							Other -->
						<entry key='depositSlipAmountMethod' value='Keyed' />
						<entry key='checkAmountMethod' value='CAR/LAR' />

						<!-- # Codeline Method could be MICR, OCR, Other -->
						<entry key='depositSlipCodelineMethod' value='Other' />
						<entry key='checkCodelineMethod' value='MICR' />

						<!-- # Aptra webservice properties -->
						<entry key='endPointAddress'
							value='http://153.71.22.5:9080/webinterface/services/remoteservices' />
						<!-- # Incase Aptra service is unavailable how many times to retry -->
						<entry key='numberOfRetries' value='1' />
						<!-- # Incase Aptra service is unavailable the retry interval in seconds -->
						<entry key='retryInterval' value='5' />

						<!-- # Generate keys -> Deposit/Transaction ID and Item IDs and set 
							into WBI request XML (for PWE) as well as CDS XML (for TM) # enableAptraDataPerfection 
							= true # enableAptraDataPerfection = false -->
						<entry key='enableAptraDataPerfection' value='true' />

						<!-- # The Deposit ID from Aptra response needs to be set into Deposit 
							Slip codeline fields 8 or 9 or 10 # This property works only when setAptraResponseintoCDS 
							property is true # The valid values can be 8 or 9 or 10 only -->
						<entry key='aptraDepositIdToDepositSlipCodeline' value='8' />

						<!-- # If aptraCaptureDRNField is 0 then CS calculated Item Id is set 
							to captureDRN field # If aptraCaptureDRNField is 1 then ScannerSequenceNumber 
							of input XML is set to captureDRN field # Can be upgraded in future if more 
							options are to be given -->
						<entry key='aptraCaptureDRNField' value='0' />

						<!-- # List of severity codes in case of failure -->
						<entry key='severityCodesForFailure' value='FATAL,ERROR' />

						<!-- # List of error codes in case of failure -->
						<entry key='errorCodesForFailure' value='200,201,300,301' />
						
						<!-- # To enable or disable the archiving functionality for Wbi request xmls -->
						<entry key='wbiArchiveEnable' value='false' />
						
						<!-- # Export Location for Sucessful Wbi Request Xml -->
						<entry key='exportLocation' value='archive/wbiExport' />
						
						<!-- # Export Location for failed Wbi Request Xml -->
						<entry key='exportLocationFailures' value='archive/wbiExportFailures' />
					</map>
				</node>
				
			<node name='DepositSlipNode'>
					<map>
						<entry key='codeline'
								value="                 d121000044d     c       96            " />
						<entry key='totalNumberOfDocs' value='{lookup(sourceLocationTable,static.NumberOfDocsCode,txn.DepositAmount),xstring,%r0r2sl}' />
						<entry key='frontImage' value='/images/creditFront.bmp' />
						<entry key='logicalPocketNumber' value='8' />
						<entry key='documentName' value='Deposit Slip' />
						<entry key='documentTypeNumber' value='1' />
						<entry key='rearImage' value='/images/creditRear.bmp' />
						<entry key='ImageEndorsementFormats' value='documentName,amount,CodeLine' />
					</map>
						
		   	</node>
		   	
		   	
		   	<node name='CashWithdrawlNode'>
					<map>
						<entry key='codeline'	value="                 d516601757d     c       94            " />
						<entry key='totalNumberOfDocs' value='{lookup(sourceLocationTable,static.NumberOfDocsCode,txn.DepositAmount),xstring,%r0r2sl}' />
						<entry key='frontImage' value='/images/debitFront.bmp' />
						<entry key='logicalPocketNumber' value='8' />
						<entry key='documentName' value='Cash Withdrawl' />
						<entry key='documentTypeNumber' value='1' />
						<entry key='rearImage' value='/images/debitRear.bmp' />
						<entry key='ImageEndorsementFormats' value='documentName,amount,CodeLine' />
					</map>
									
			</node>
			
		</node>
			
			;]]>
</value>

<editPattern>NONE</editPattern>

<readOnly>false</readOnly>

<version>3</version>

</com.ncr.payments.configuration.ConfigurationItem>

</list>