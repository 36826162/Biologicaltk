Biologicaltk
============

  Public Sub StoreData()


        Dim Title As String
        Dim Initials As String
        Dim Surname As String
        Dim Address As String
        Dim BirthDate As DateTime
        Dim Gender As String

        DateTimePicker1.CustomFormat = "dd-mm-yyyy"
        BirthDate = Convert.ToDateTime(DateTimePicker1.Value.ToShortDateString())

        Title = cbmTitle.SelectedItem
        ' lbTitle.Items.Add(Title)
        Initials = txtInitials.Text
        Surname = txtSurname.Text
        Address = txtAddress.Text

        If (rbnMale.Checked = True) Then
            Gender = "Male"
        Else
            Gender = "Female"
        End If


        If Title <> String.Empty And Initials <> String.Empty And Surname <> String.Empty And Address <> String.Empty Then
            Try


                Dim data() As Integer = New Integer() {}
                'Dim data() As Integer
                ' Open file for writing text 
                Dim writer As StreamWriter = File.AppendText("C:\StudTextFile.txt")

                 writer.Write("{0},{1},{2},{3},{4},{5},{6}" & vbCrLf & "", GetNextNum(), BirthDate, Title, Initials, Surname, Address, Gender)

                'Dim val As string
                Dim val As String
                For Each val In data
                    writer.Write("," & val)
                Next
                ' Close StreamWriter when done 
                writer.Close()


                MessageBox.Show("Record Saved.")

                lblAutoGenNum.Text = GetNextNum()

            Catch ex As Exception

                MessageBox.Show(ex.Message + "Error occurred!")

            Finally

                ClearFields()

            End Try
        Else
            MessageBox.Show("Please enter all fields.")
        End If

    End Sub
