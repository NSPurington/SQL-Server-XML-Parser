/****** Object:  UserDefinedFunction [dbo].[MustangReportBuild]    Script Date: 1/10/2020 7:49:40 PM ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO

ALTER FUNCTION [dbo].[MustangReportBuild]
(	
	@Id uniqueidentifier
)
RETURNS TABLE 
AS
RETURN 
(
	WITH XMLNAMESPACES(DEFAULT 'http://www.ebay.com/marketplace/search/v1/services') 

	SELECT
		itemId			= Col.value('itemId[1]','varchar(255)')  
		,Date			= Col.value('(listingInfo/endTime)[1]','varchar(255)')  
		,location		= LEFT(Col.value('location[1]', 'varchar(255)'), LEN(Col.value('(location)[1]', 'varchar(255)')) -4)
		,BidCount		= Col.value('(sellingStatus/bidCount)[1]', 'varchar(255)')
		,SoldPrice		= Col.value('(sellingStatus/currentPrice)[1]', 'varchar(255)')
		,Convertible	= CASE WHEN Col.value('title[1]','varchar(255)') LIKE '%convert%' THEN 'Y' ELSE 'N' END 
		,Fastback		= CASE WHEN Col.value('title[1]','varchar(255)') LIKE '%fastback%' THEN 'Y' ELSE 'N' END 
		,Image			= Col.value('galleryURL[1]', 'varchar(255)')


    FROM
		dbo.MustangSalesImport
		CROSS APPLY ImportData.nodes('/findCompletedItemsResponse/searchResult/item') as T(Col)

	WHERE
		MustangSalesImport.Id = @Id
	)
