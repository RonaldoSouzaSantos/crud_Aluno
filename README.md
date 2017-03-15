# crud_Aluno
#Form1.Disigner.cs

namespace Sistema_Crud_Aluno
{
    partial class dem_Crud
    {
        /// <summary>
        /// Required designer variable.
        /// </summary>
        private System.ComponentModel.IContainer components = null;

        /// <summary>
        /// Clean up any resources being used.
        /// </summary>
        /// <param name="disposing">true if managed resources should be disposed; otherwise, false.</param>
        protected override void Dispose(bool disposing)
        {
            if (disposing && (components != null))
            {
                components.Dispose();
            }
            base.Dispose(disposing);
        }

        #region Windows Form Designer generated code

        /// <summary>
        /// Required method for Designer support - do not modify
        /// the contents of this method with the code editor.
        /// </summary>
        private void InitializeComponent()
        {
            this.SuspendLayout();
            // 
            // dem_Crud
            // 
            this.ClientSize = new System.Drawing.Size(553, 299);
            this.Name = "dem_Crud";
            this.Load += new System.EventHandler(this.dem_Crud_Load_1);
            this.ResumeLayout(false);

        }

        #endregion

        private System.Windows.Forms.Timer timer1;
        private System.Windows.Forms.Panel panel1;
        private System.Windows.Forms.ToolStrip toolStrip1;
        private System.Windows.Forms.StatusStrip statusStrip1;
        private System.Windows.Forms.Panel panel2;
        private System.Windows.Forms.TabControl tabControl1;
        private System.Windows.Forms.TabPage tabPage1;
        private System.Windows.Forms.TabPage tabPage2;
        private System.Windows.Forms.TabPage tabPage3;
        private System.Windows.Forms.TabPage tabPage4;
        private System.Windows.Forms.ToolStripButton toolStripButton1;
        private System.Windows.Forms.ToolStripButton toolStripButton2;
        private System.Windows.Forms.ToolStripButton toolStripButton3;
        private System.Windows.Forms.ToolStripSeparator toolStripSeparator1;
        private System.Windows.Forms.ToolStripButton toolStripButton4;
        private System.Windows.Forms.ToolStripButton toolStripButton5;
        private System.Windows.Forms.ToolStripStatusLabel lbDateTime;
    }
}

#sisDBADM

using System;
using System.Collections.Generic;
using System.Collections;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Data;
using System.Data.SqlClient;


namespace Sistema_Crud_Aluno
{
    class sisDBADM
    {
        private const string _strCon = @"Data Source=SAMSUNG-NOTE;Initial Catalog=crud_aluno;Integrated Security=True";
        private string vsql = string.Empty;
        SqlConnection objCon = null;
        
        #region "METODOS DE CONEXÃO COM BANCO"
        private bool conectar()
        {
            objCon = new SqlConnection(_strCon);
            try
            {
                objCon.Open();
                return true;
            }
            catch
            {
                return false;
            }


        }

        private bool desconectar()
        {
            if(objCon.State != ConnectionState.Closed)
            {
                objCon.Close();
                return true;
            }
            else
            {
                objCon.Dispose();
                return false;
            }
        }
        #endregion

       // #region "METODOS DE EXECUÇÃO DO SQL"
        public bool Insert(ArrayList p_arrInsert)
        {
            vsql = "INSERT INTO ALUNOS([nome], [idade], [endereco], [telefone], [email], [cidade], [uf], [nome_pai], [nome_mae])" +
                        "VALUES(@nome, @idade, @endereco, @telefone, @email, @cidade, @uf, @nome_pai, @nome_mae)";
            SqlCommand objcmd = null;


            if (this.conectar())
            {
                try
                {
                    objcmd = new SqlCommand(vsql, objCon);
                    objcmd.Parameters.Add(new SqlParameter("@nome", p_arrInsert[0]));
                    objcmd.Parameters.Add(new SqlParameter("@idade", p_arrInsert[1]));
                    objcmd.Parameters.Add(new SqlParameter("@endereco", p_arrInsert[2]));
                    objcmd.Parameters.Add(new SqlParameter("@telefone", p_arrInsert[3]));
                    objcmd.Parameters.Add(new SqlParameter("@email", p_arrInsert[4]));
                    objcmd.Parameters.Add(new SqlParameter("@cidade", p_arrInsert[5]));
                    objcmd.Parameters.Add(new SqlParameter("@uf", p_arrInsert[6]));
                    objcmd.Parameters.Add(new SqlParameter("@nome_pai", p_arrInsert[7]));
                    objcmd.Parameters.Add(new SqlParameter("@nome_mae", p_arrInsert[8]));

                    objcmd.ExecuteNonQuery();

                    return true;
                }

                catch(SqlException sqlerr)
                {
                    throw sqlerr;
                }

                finally
                {
                    this.desconectar();
                }
            }
            else
            {
                return false;
            }


        }
       /* public bool Update()
        {

        }
        public bool Delete()
        {
        
        }
        #endregion

        #region "METODOS QUE LISTAGRID E FAZ PESQUISA"
        public DateTime ListaGrid()
        {

        }
        public DateTime Pesquisar()
        {

        }
        #endregion
        */

    }
}


#Program.cs
using System;
using System.Collections.Generic;
using System.Linq;
using System.Threading.Tasks;
using System.Windows.Forms;

namespace Sistema_Crud_Aluno
{
    static class Program
    {
        /// <summary>
        /// The main entry point for the application.
        /// </summary>
        [STAThread]
        static void Main()
        {
            Application.EnableVisualStyles();
            Application.SetCompatibleTextRenderingDefault(false);
            Application.Run(new dem_Crud());
        }
    }
}


