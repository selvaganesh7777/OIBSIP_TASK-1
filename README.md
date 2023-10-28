XMLDemoPage.aspx.cs
using System;
using System.Collections.Generic;
using System.Linq;
using System.Web;
using System.Web.UI;
using System.Web.UI.WebControls;
using System.Xml;

namespace XMLDemo
{
    public partial class XMLDemoPage : System.Web.UI.Page
    {
        protected void Page_Load(object sender, EventArgs e)
        {

        }

        protected void btnRead_Click(object sender, EventArgs e)
        {
            XmlReader red = XmlReader.Create(@"D:\XMLDemoData\XMLFile.xml");
            while (red.Read())
            {
                if(red.NodeType.Equals(XmlNodeType.Element))
                {
                    lblDetails.Text += "<br/>" + lblDetails.Text + red.Name;
                }
            }
            red.Close();
        }

        protected void btnWrite_Click(object sender, EventArgs e)
        {
            XmlWriterSettings set = new XmlWriterSettings();
            set.Indent = true;
            XmlWriter wr = XmlWriter.Create(@"D:\XMLDemoData\XMLFile.xml", set);
            wr.WriteStartDocument();
            wr.WriteComment("Example of write a XML Document");
            wr.WriteStartElement(txtName.Text);
            wr.WriteEndElement();
            wr.WriteEndDocument();
            wr.Flush();
            wr.Close();
        }
    }
}


XMLDemoPage.aspx
<%@ Page Language="C#" AutoEventWireup="true" CodeBehind="XMLDemoPage.aspx.cs" Inherits="XMLDemo.XMLDemoPage" %>

<!DOCTYPE html>

<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
    <title></title>
</head>
<body>
    <form id="form1" runat="server">
        <div>
            <asp:Button runat="server" Text="XML Read" ID="btnRead" onClick ="btnRead_Click"/><br />
            <asp:Label runat="server" Text="" ID="lblDetails" /><br />
            <asp:TextBox runat="server" ID="txtName" /><br />
             <asp:Button runat="server" Text="XML Write" ID="btnWrite" onClick="btnWrite_Click"/><br />
        </div>
    </form>
</body>
</html>
