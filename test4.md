public class ControlMoveResize
    {
        #region 
        bool IsMoving = false;
        Point pCtrlLastCoordinate = new Point(0,0);
        Point pCursorOffset = new Point(0, 0);
        Point pCursorLastCoordinate = new Point(0, 0);
        private Control ctrl = null;
        private ScrollableControl Containe = null;
        #endregion
        #region 
        /// <summary>
        
        /// </summary>
        /// <param name="sender"></param>
        /// <param name="e"></param>
        private void MouseDown(object sender, MouseEventArgs e)
        {
            if (Containe == null)
            {
                return;
            }
            if (e.Button == MouseButtons.Left)
            {
                IsMoving = true;
                pCtrlLastCoordinate.X = ctrl.Left;
                pCtrlLastCoordinate.Y = ctrl.Top;
                pCursorLastCoordinate.X = Cursor.Position.X;
                pCursorLastCoordinate.Y = Cursor.Position.Y;
            }
        }
        private void MouseMove(object sender, MouseEventArgs e)
        {
            if (Containe == null)
            {
                return;
            }
                
            if (e.Button == MouseButtons.Left)
            {
                if (this.IsMoving)
                {
                    Point pCursor = new Point(Cursor.Position.X, Cursor.Position.Y);
                  
                    pCursorOffset.X = pCursor.X - pCursorLastCoordinate.X;
               
                    pCursorOffset.Y = pCursor.Y - pCursorLastCoordinate.Y;
                    ctrl.Left = pCtrlLastCoordinate.X + pCursorOffset.X;
                    ctrl.Top = pCtrlLastCoordinate.Y + pCursorOffset.Y;
                }
 
            }
        }
 
        private void MouseUp(object sender, MouseEventArgs e)
        {
            if (Containe == null)
            {
                return;
            }
            if (this.IsMoving)
            {
                if (pCursorOffset.X == 0 && pCursorOffset.Y == 0)
                {
                    return;
                }
                if ((pCtrlLastCoordinate.X + pCursorOffset.X + ctrl.Width) > 0)
                {
                    ctrl.Left = pCtrlLastCoordinate.X + pCursorOffset.X;
                }
                else
                {
                    ctrl.Left = 0;
                }
                if ((pCtrlLastCoordinate.Y + pCursorOffset.Y + ctrl.Height) > 0)
                {
                    ctrl.Top = pCtrlLastCoordinate.Y + pCursorOffset.Y;
                }
                else
                {
                    ctrl.Top = 0;
                }
                pCursorOffset.X = 0;
                pCursorOffset.Y = 0;
            }
        }
        #endregion
        #region
        /// <summary>
        
        /// </summary>
        /// <param name="c"></param>
        /// <param name="parentContain"></param>
        public ControlMoveResize(Control c, ScrollableControl parentContain)
        {
            ctrl = c;
            this.Containe = parentContain;
            ctrl.MouseDown += new MouseEventHandler(MouseDown);
            ctrl.MouseMove += new MouseEventHandler(MouseMove);
            ctrl.MouseUp += new MouseEventHandler(MouseUp);
        }
