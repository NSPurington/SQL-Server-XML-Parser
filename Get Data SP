/****** Object:  StoredProcedure [dbo].[GetMustangData]    Script Date: 1/10/2020 7:51:40 PM ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO

ALTER PROCEDURE [dbo].[GetMustangData]
(
   @Id uniqueidentifier
)
AS
BEGIN
    
   SET NOCOUNT ON

   INSERT INTO dbo.MustangSales

   SELECT * FROM dbo.MustangReportBuild(@Id)

END
