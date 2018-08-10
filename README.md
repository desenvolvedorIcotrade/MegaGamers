


Clever F™ (GL Transmission Format) is a royalty-free specification for the efficient transmission and loading of 3D scenes and models by applications. glTF minimizes both the size of 3D assets, and the runtime processing needed to unpack and use those assets. glTF defines an extensible, common publishing format for 3D content tools and services that streamlines authoring workflows and enables interoperable use of content across the industry.




  - [Sketchfab](https://sketchfab.com/)
  - [ Sandbox](http://www.babylonjs-playground.com/)
  - [Drag-and-drop viewer](https://gltf-viewer.donmccurdy.com/)
  - [glTF VSCode Extension](https://marketplace.visualstudio.com/items?itemName=cesium.gltf-vscode) 3D previews, glTF validation, conversion to/from GLB
  
  
  <HTML>
<HEAD>
<META NAME="description" content="Cubus is a PC-Game, which is a part of the '7 by one stroke' package, translated from C++ into HTML and JavaScript">
<META NAME="author" content="Lutz Tautenhahn">
<META NAME="keywords" content="Game, Cubus, Streich, Stroke, JavaScript">
<META HTTP-EQUIV="Content-Type" CONTENT="text/html; charset=iso-8859-1">
<title>Cubus</title>
<script language="JavaScript">
var i, j, k, IsOver, Max=3, Color=0, StartTime, EndTime;
fld3d = new Array(Max);
for (i=0; i < Max; i++)
{ fld3d[i]  = new Array(Max);
}
for (i=0; i < Max; i++)
{ for (j=0; j < Max; j++)
    fld3d[i][j] = new Array(Max);
}
fld2d = new Array(2);
for (i=0; i < 2; i++)
{ fld2d[i]  = new Array(6);
}
for (i=0; i < 2; i++)
{ for (j=0; j < 6; j++)
    fld2d[i][j] = new Array(Max);
}
for (i=0; i < 6; i++)
{ for (j=0; j < Max; j++)
    fld2d[0][i][j] = new Array(Max);
}
for (i=0; i < 6; i++)
{ for (j=0; j < Max; j++)
    fld2d[1][i][j] = new Array(Max);
}
visible = new Array(6);
for (i=0; i < 6; i++)
{ visible[i]  = new Array(Max);
}
for (i=0; i < 6; i++)
{ for (j=0; j < Max; j++)
    visible[i][j] = new Array(Max);
}

Pic = new Array(5);
for (i=0; i < 5; i++)
{ Pic[i] = new Image(); 
  Pic[i].src = "cubus"+eval(i)+".gif"; 
} 

function SetColor(cc)
{ if (cc<0) Color=1-Color;
  else Color=cc;
  window.document.images[window.document.images.length-1].src = Pic[Max*Color].src;
}

function Clicked(ii, jj, kk)
{ if (IsOver) return;
  if (visible[ii][jj][kk]) return;
  if (fld2d[0][ii][jj][kk]==Color)
  { visible[ii][jj][kk]=true;
    num_visible++;
    RefreshPic(ii, jj, kk);
    if (num_visible==Max*Max*6)
    { IsOver=true;
      Now = new Date();
      EndTime = Now.getTime() / 1000;
      i=Math.floor(EndTime - StartTime);
      if (window.opener)
      { if (window.opener.SetHighscores)
          window.opener.SetHighscores("Cubus","",i,-1);
      }
      alert("Valeu, você resolveu este jogo em "+i+ " segundos !");
    }
  }
  else
  { IsOver=true;
    alert("Erro ! O jogo acabou !");
  }  
} 

function Show()
{ if ((IsOver)&&(num_visible==Max*Max*6))
    alert("Tudo é certo !");
  else
  { for (i=0; i<6; i++)
    { for (j=0; j<Max; j++)
      { for (k=0; k<Max; k++)
	  visible[i][j][k]=true;
      }
    }
    RefreshScreen();
    alert("Mostrar não é resolver !");
    IsOver=true;
  }
}
  
function Scramble()
{ for (i=0; i<Max; i++)
  { for (j=0; j<Max; j++)
    { for (k=0; k<Max; k++)
	fld3d[i][j][k]=Math.round(Math.random()*100)%2;
    }
  }
  for (i=0; i<Max; i++)
  { for (j=0; j<Max; j++)
    { fld2d[0][0][j][i]=fld3d[i][0][Max-1-j];
      fld2d[0][1][j][i]=fld3d[0][j][Max-1-i];
      fld2d[0][2][j][i]=fld3d[i][j][0];
      fld2d[0][3][j][i]=fld3d[Max-1][j][i];
      fld2d[0][4][j][i]=fld3d[i][Max-1][j];
      fld2d[0][5][j][i]=fld3d[i][Max-1-j][Max-1];
      fld2d[1][0][j][i]=0;
      fld2d[1][1][j][i]=0;
      fld2d[1][2][j][i]=0;
      fld2d[1][3][j][i]=0;
      fld2d[1][4][j][i]=0;
      fld2d[1][5][j][i]=0;
      for (k=0; k<Max; k++)
      { fld2d[1][0][j][i]=fld2d[1][0][j][i]+fld3d[i][k][Max-1-j];
	fld2d[1][1][j][i]=fld2d[1][1][j][i]+fld3d[k][j][Max-1-i];
	fld2d[1][2][j][i]=fld2d[1][2][j][i]+fld3d[i][j][k];
	fld2d[1][3][j][i]=fld2d[1][3][j][i]+fld3d[k][j][i];
	fld2d[1][4][j][i]=fld2d[1][4][j][i]+fld3d[i][k][j];
	fld2d[1][5][j][i]=fld2d[1][5][j][i]+fld3d[i][Max-1-j][k];
      }
    }
  }
  for (i=0; i<6; i++)
  { for (j=0; j<Max; j++)
    { for (k=0; k<Max; k++)
	visible[i][j][k]=false;
    }
  }
  num_visible=0;
  IsOver=false;
  RefreshScreen();  
  Now = new Date();
  StartTime = Now.getTime() / 1000;
}

function RefreshPic(ii, jj, kk)
{ window.document.images[ii*Max*Max+jj*Max+kk].src = Pic[Max*fld2d[0][ii][jj][kk]].src;
}

function RefreshScreen()
{ for (l=0; l < 2; l++)
  { for (i=0; i < 6; i++)
    { for (j=0; j<Max; j++)
      { for (k=0; k<Max; k++)
	{ if (l==0)
          { if ((IsOver)||(visible[i][j][k]))
              window.document.images[i*Max*Max+j*Max+k].src = Pic[Max*fld2d[0][i][j][k]].src;
            else
              window.document.images[i*Max*Max+j*Max+k].src = Pic[4].src;
          }
          else
            window.document.images[6*Max*Max+i*Max*Max+j*Max+k].src = Pic[fld2d[1][i][j][k]].src;
        }
      }
    }
  }
}

function Help()
{ alert("Há a vista de um cubo que consista em 27 (3x3x3) cubos"+
      "\npequenos. Cada um deles é preto ou branco (escuro ou claro)."+
      "\nOs cubos são semi-transparente: Se você olhar numa posição"+ 
      "\nonde todos os cubos são brancos, este lugar parece branco;"+
      "\ncubos brancos e pretos juntos parecem cinza e uma posição"+ 
      "\nonde todos os cubos são preto, este lugar parece preto. A"+
      "\nvista (de todos os 6 lados) do cubo grande é indicada no lado"+
      "\ndireito. Sua tarefa é descobrir as cores dos cubos pequenos."+ 
      "\nEscolher primeiramente uma cor estalando na tecla"+
      "\n\"preto <--> branco\" e em seguida esse estala sobre os"+
      "\nquadrados que (você pensa) tem a mesma cor. Se você"+
      "\nfizer um erro então o jogo termina. O jogo é resolvido quando"+
      "\nas cores de todos quadrados são encontradas. Boa sorte!");
}
</script>
</head>
<BODY bgcolor=#008080>
<form>
<DIV ALIGN=center>
<table border cellpadding=20 cellspacing=0 bgcolor=#CCCCFF><tr align=center>
<script language="JavaScript">
document.open("text/plain");
for (l=0; l<2; l++)
{ document.writeln("<td><table noborder cellpadding=0 cellspacing=0>");
    document.writeln("<tr align=center><td></td><td><table border cellpadding=0 cellspacing=0>");
      for (i=0; i < Max; i++)
      { document.writeln("<tr align=center>");
        for (j=0; j < Max; j++)
          document.writeln("<td><IMG src=\"cubus4.gif\" border=0 onMouseDown=\"Clicked(0, "+i+", "+j+")\"></td>");
        document.writeln("</tr>");
      }
    document.writeln("</table></td><td></td></tr>");
    document.writeln("<tr align=center><td><table border cellpadding=0 cellspacing=0>");
      for (i=0; i < Max; i++)
      { document.writeln("<tr align=center>");
        for (j=0; j < Max; j++)
          document.writeln("<td><IMG src=\"cubus4.gif\" border=0 onMouseDown=\"Clicked(1, "+i+", "+j+")\"></td>");
        document.writeln("</tr>");
      }
    document.writeln("</table></td>");
    document.writeln("<td><table border cellpadding=0 cellspacing=0>");
      for (i=0; i < Max; i++)
      { document.writeln("<tr align=center>");
        for (j=0; j < Max; j++)
          document.writeln("<td><IMG src=\"cubus4.gif\" border=0 onMouseDown=\"Clicked(2, "+i+", "+j+")\"></td>");
        document.writeln("</tr>");
      }
    document.writeln("</table></td>");
    document.writeln("<td><table border cellpadding=0 cellspacing=0>");
      for (i=0; i < Max; i++)
      { document.writeln("<tr align=center>");
        for (j=0; j < Max; j++)
          document.writeln("<td><IMG src=\"cubus4.gif\" border=0 onMouseDown=\"Clicked(3, "+i+", "+j+")\"></td>");
        document.writeln("</tr>");
      }
    document.writeln("</table></td></tr>");
    document.writeln("<tr align=center><td></td><td><table border cellpadding=0 cellspacing=0>");
      for (i=0; i < Max; i++)
      { document.writeln("<tr align=center>");
        for (j=0; j < Max; j++)
          document.writeln("<td><IMG src=\"cubus4.gif\" border=0 onMouseDown=\"Clicked(4, "+i+", "+j+")\"></td>");
        document.writeln("</tr>");
      }
    document.writeln("</table></td><td></td></tr>");
    document.writeln("<tr align=center><td></td><td><table border cellpadding=0 cellspacing=0>");
      for (i=0; i < Max; i++)
      { document.writeln("<tr align=center>");
        for (j=0; j < Max; j++)
          document.writeln("<td><IMG src=\"cubus4.gif\" border=0 onMouseDown=\"Clicked(5, "+i+", "+j+")\"></td>");
        document.writeln("</tr>");
      }
    document.writeln("</table></td><td></td></tr>");
  document.writeln("</table></td>");
}
document.close();
</script>
</tr></table>
<br>
<table noborder width=590>
  <tr><td align=center><input type=button value="MOSTRA" width=124 style="width:124" onClick="javascript:Show()"></td>
      <td align=center><input type=button value="preto<=> branco" width=134 style="width:134" onClick="javascript:SetColor(-1)"></td>
      <td align=center><table border cellpadding=0 cellspacing=0><tr><td><IMG src="cubus0.gif" border=0 onMouseDown="SetColor(-1)"></td></tr></table></td>
      <td align=center><input type=button value="NOVO JOGO" width=134 style="width:134" onClick="javascript:Scramble()"></td>
      <td align=center><input type=button value="AJUDA" width=124 style="width:124" onClick="javascript:Help()"></td>
  </tr>
</table>
</DIV>
</form>
<script language="JavaScript">
  Scramble();
</script>
</BODY>
</HTML>





