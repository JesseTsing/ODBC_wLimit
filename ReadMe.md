# a bug fix to Amibroker's ODBC Plugin
## the original does not implement "limit" feature,causing a huge latency in realtime data streaming 



mainly changed following segment:
```
if( 1 /*GLOBAL_bUseLimitClause*/ )
	{
		
		switch(g_oData.m_iServerType)
		{
			//generic and mysql
		case 0:
		case 1:
			{
			CString oLimit;
			oLimit.Format(" LIMIT %d", nSize );
			oSQL += oLimit;
			break;	
			}
			// msSQL
		case 2:
			{
			CString oLimit;
			oLimit.Format("SELECT TOP %d ", nSize );
			oSQL.Replace("SELECT",oLimit);
			break;
			}
		default:
			AfxMessageBox("unsupport SELECT :" + oSQL);
		

		}
	}

```