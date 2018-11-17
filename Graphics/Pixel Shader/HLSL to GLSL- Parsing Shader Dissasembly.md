# HLSL to GLSL: Parsing Shader Dissasembly

http://www.sebbylive.com/2011/10/02/hlsl-to-glsl-parsing-shader-dissasembly

Finally got around to writing my first in-depth post about my HLSL to GLSL translation work. In this first post, I go over some of the basics and the generation of a grammar that will take basic dissasembled HLSL into a more usable binary representation. To serve as an example, here is a basic HLSL sample taken from the DirectX SDK...

	//--------------------------------------------------------------------------------------
	// File: BasicHLSL.fx
	//
	// The effect file for the BasicHLSL sample.
	//
	// Copyright (c) Microsoft Corporation. All rights reserved.
	//--------------------------------------------------------------------------------------
	
	//--------------------------------------------------------------------------------------
	// Global variables
	//--------------------------------------------------------------------------------------
	float4 g_MaterialAmbientColor;      // Material's ambient color
	float4 g_MaterialDiffuseColor;      // Material's diffuse color
	int g_nNumLights;
	
	float3 g_LightDir[3];               // Light's direction in world space
	float4 g_LightDiffuse[3];           // Light's diffuse color
	float4 g_LightAmbient;              // Light's ambient color
	
	texture g_MeshTexture;              // Color texture for mesh
	
	float    g_fTime;                   // App's time in seconds
	float4x4 g_mWorld;                  // World matrix for object
	float4x4 g_mWorldViewProjection;    // World * View * Projection matrix
	
	//--------------------------------------------------------------------------------------
	// Texture samplers
	//--------------------------------------------------------------------------------------
	sampler MeshTextureSampler =
	sampler_state
	{
	    Texture = <g_MeshTexture>;
	    MipFilter = LINEAR;
	    MinFilter = LINEAR;
	    MagFilter = LINEAR;
	};
	
	//--------------------------------------------------------------------------------------
	// Vertex shader output structure
	//--------------------------------------------------------------------------------------
	struct VS_OUTPUT
	{
	    float4 Position   : POSITION;   // vertex position
	    float4 Diffuse    : COLOR0;     // vertex diffuse color (note that COLOR0 is clamped from 0..1)
	    float2 TextureUV  : TEXCOORD0;  // vertex texture coords
	};
	
	//--------------------------------------------------------------------------------------
	// This shader computes standard transform and lighting
	//--------------------------------------------------------------------------------------
	VS_OUTPUT RenderSceneVS( float4 vPos : POSITION,
	                         float3 vNormal : NORMAL,
	                         float2 vTexCoord0 : TEXCOORD0,
	                         uniform int nNumLights,
	                         uniform bool bTexture,
	                         uniform bool bAnimate )
	{
	    VS_OUTPUT Output;
	    float3 vNormalWorldSpace;
		
	    float4 vAnimatedPos = vPos;
		
	    // Animation the vertex based on time and the vertex's object space position
	    if( bAnimate )
			vAnimatedPos += float4(vNormal, 0) * (sin(g_fTime+5.5)+0.5)*5;
			
	    // Transform the position from object space to homogeneous projection space
	    Output.Position = mul(vAnimatedPos, g_mWorldViewProjection);
		
	    // Transform the normal from object space to world space
	    vNormalWorldSpace = normalize(mul(vNormal, (float3x3)g_mWorld)); // normal (world space)
		
	    // Compute simple directional lighting equation
	    float3 vTotalLightDiffuse = float3(0,0,0);
	    for(int i=0; i<nNumLights; i++ )
	        vTotalLightDiffuse += g_LightDiffuse[i] * max(0,dot(vNormalWorldSpace, g_LightDir[i]));
			
	    Output.Diffuse.rgb = g_MaterialDiffuseColor * vTotalLightDiffuse +
	                         g_MaterialAmbientColor * g_LightAmbient;
	    Output.Diffuse.a = 1.0f; 
		
	    // Just copy the texture coordinate through
	    if( bTexture )
	        Output.TextureUV = vTexCoord0;
	    else
	        Output.TextureUV = 0; 
			
	    return Output;
	}
	
	//--------------------------------------------------------------------------------------
	// Pixel shader output structure
	//--------------------------------------------------------------------------------------
	struct PS_OUTPUT
	{
	    float4 RGBColor : COLOR0;  // Pixel color
	};
	
	//--------------------------------------------------------------------------------------
	// This shader outputs the pixel's color by modulating the texture's
	//       color with diffuse material color
	//--------------------------------------------------------------------------------------
	PS_OUTPUT RenderScenePS( VS_OUTPUT In,
	                         uniform bool bTexture )
	{
	    PS_OUTPUT Output;
		
	    // Lookup mesh texture and modulate it with diffuse
	    if( bTexture )
	        Output.RGBColor = tex2D(MeshTextureSampler, In.TextureUV) * In.Diffuse;
	    else
	        Output.RGBColor = In.Diffuse;
			
	    return Output;
	}

Since several of the uniform constants, are not set, the shader does simplify somewhat and the generated dissasembly is included below.

	//
	// Generated by Microsoft (R) HLSL Shader Compiler 9.29.952.3111
	//
	// Parameters:
	//
	//   bool $bAnimate;
	//   bool $bTexture;
	//   int $nNumLights;
	//   float4 g_LightAmbient;
	//   float4 g_LightDiffuse[3];
	//   float3 g_LightDir[3];
	//   float4 g_MaterialAmbientColor;
	//   float4 g_MaterialDiffuseColor;
	//   float g_fTime;
	//   float4x4 g_mWorld;
	//   float4x4 g_mWorldViewProjection;
	//
	//
	// Registers:
	//
	//   Name                   Reg   Size
	//   ---------------------- ----- ----
	//   g_mWorldViewProjection c0       4
	//   g_LightDir             c4       3
	//   g_LightDiffuse         c7       3
	//   g_mWorld               c10      3
	//   g_MaterialAmbientColor c13      1
	//   g_MaterialDiffuseColor c14      1
	//   g_LightAmbient         c15      1
	//   g_fTime                c16      1
	//   $nNumLights            c17      1
	//   $bTexture              c18      1
	//   $bAnimate              c19      1
	//
	
	    vs_3_0
	    def c20, 5.5, 0.159154937, 0.5, 0
	    def c21, 6.28318548, -3.14159274, 5, 0
	    def c22, 0, 1, 2, 0
	    dcl_position v0  // vPos<0,1,2,3>
	    dcl_normal v1  // vNormal<0,1,2>
	    dcl_texcoord v2  // vTexCoord0<0,1>
	    dcl_position o0
	    dcl_color o1
	    dcl_texcoord o2.xy
		
	#line 70 "C:\Projects\HLSL2GLSLASM\HLSL2GLSLWin\bin\Debug\memory"
	    mov r0.x, c20.x
	    add r0.x, r0.x, c16.x
	    mad r0.x, r0.x, c20.y, c20.z
	    frc r0.x, r0.x
	    mad r0.x, r0.x, c21.x, c21.y
	    sincos r1.y, r0.x
	    add r0.w, r1.y, c20.z
	    mul r0.xyz, r0.w, v1
	    mul r0, r0, c19.x
	    mad r0, r0, c21.zzzw, v0  // ::vAnimatedPos<0,1,2,3>
		
	#line 73
	    dp4 o0.x, r0, c0  // ::RenderSceneVS<0>
	    dp4 o0.y, r0, c1  // ::RenderSceneVS<1>
	    dp4 o0.z, r0, c2  // ::RenderSceneVS<2>
	    dp4 o0.w, r0, c3  // ::RenderSceneVS<3>
		
	#line 76
	    dp3 r0.x, v1, c10
	    dp3 r0.y, v1, c11
	    dp3 r0.z, v1, c12
	    nrm r1.xyz, r0  // ::vNormalWorldSpace<0,1,2>
		
	#line 81
	    dp3 r0.x, r1, c4
	    max r0.x, r0.x, c20.w
	    mul r0.xyz, r0.x, c7  // ::vTotalLightDiffuse<0,1,2>
	    dp3 r0.w, r1, c5
	    dp3 r1.x, r1, c6
	    max r1.x, r1.x, c20.w
	    mul r1.xyz, r1.x, c9
	    max r0.w, r0.w, c20.w
	    mul r2.xyz, r0.w, c8
	    mov r3.xyz, c22  // ::i<0>
	    slt r3.xyz, r3, c17.x  // ::i<0>
	    mul r2.xyz, r2, r3.y
	    mad r0.xyz, r3.x, r0, r2  // ::vTotalLightDiffuse<0,1,2>
	    mad r0.xyz, r3.z, r1, r0  // ::vTotalLightDiffuse<0,1,2>
		
	#line 84
	    mov r1.xyz, c13  // ::g_MaterialAmbientColor<0,1,2>
	    mul r1.xyz, r1, c15
	    mad o1.xyz, c14, r0, r1  // ::RenderSceneVS<4,5,6>
		
	#line 88
	    mul o2.xy, c18.x, v2  // ::RenderSceneVS<8,9>
		
	#line 84
	    mov o1.w, c22.y  // ::RenderSceneVS<7>
		
	// approximately 46 instruction slots used

The actual structure of the dissasembly file is not documented although the DirectX documentation does include most of the documentation for the meaning of the ASM instructions. However, the structure of the assembly file is straightforward and was easy to reverse engineer.

Using C#, I've decided to settle on <a href="/web/20121008015456/http://www.antlr.org/">Antlr </a>as my parser generator. Antly can generate grammars and lexers in different languages including C#. Although Antlr's syntax deviates slightly from the standard Lexx/Yacc grammar, it is still in a similar <a href="/web/20121008015456/http://en.wikipedia.org/wiki/Backus%E2%80%93Naur_Form">BNF </a>form along with additional annotations which can serve as syntaxic and semantic predicated. I decided to include the grammar for reference but since it is fairly lengthy, I've included it at the end of the post to avoid clutter.

With Antlr, I am not translating on the fly but rather using a AST grammar to generate a syntax tree which in essence is a binary representation of the source code which is obviously easier to handle in code than the text form. This tree is further processed into a usable form (next post) and is then translated into GLSL form.

Here is a snapshot of what the tree looks like from within my test application.

http://www.sebbylive.com/wp-content/uploads/2011/10/sm3AST.png

The generated AST is still fairly general with items such as register references being leaf nodes of the tree. To make the translation process less cumbersome, I decided to add another processing step before the translation occurs. This step takes the general AST and compacts it into a more specialized tree where each node is represented by a class for each type of operation, this in turns makes the translation process less centralized and easier to approach. The creation of the compact tree will be the topic of my next post...

Finally, as promised here is the grammar I use so far to process the shader dissasembly into an AST. Note that there is some Shader Model 4/5 constructs in the grammar as I am working on adding support for DX10 shaders in my tool. But as of right now, only Shader Model 3 support fully works.

	grammar HLSLAST;
	
	options {
	    language=CSharp3;
	    TokenLabelType=CommonToken;
	    output=AST;
	    ASTLabelType=CommonTree;
	}
	
	tokens
	{
		PROGRAM;
		OP_DP3; OP_DP4; OP_MUL; OP_MAX; OP_MOV; OP_MOVA; OP_ADD; OP_CRS; OP_MIN; OP_SUB; OP_ABS; OP_DSX; OP_DSY; OP_EXP; OP_FRC;
		OP_LOG; OP_NRM; OP_POW; OP_RCP; OP_RSQ; OP_SINCOS; OP_MAD; OP_CMP; OP_LRP; OP_BREAK; OP_DST; OP_IF; OP_CALL; OP_LABEL;
		OP_SGE; OP_SGN; OP_SLT; OP_LOOP; OP_REP; OP_TEXKILL; OP_DP2ADD;
		OP_SAMPLE; OP_INDEX_PLUS; OP_DEF; OP_IF_INSTR; OP_IF_ELSE_INSTR; OP_LOOP_INSTR; OP_DCL; OP_DEBUG_LINE;
		OP4_AND; OP4_BREAK; OP4_CONTINUE; OP4_SWITCH; OP4_MAD; OP4_IMAD; OP4_UMAD; OP4_ADD; OP4_DP2; OP4_DP3; OP4_DP4; OP4_DIV;
		OP4_EQ; OP4_GE; OP4_LT; OP4_IADD; OP4_IEQ; OP4_IGE; OP4_ILT; OP4_IMUL; OP4_IMIN; OP4_INE; OP4_ISHL; OP4_ISHR; OP4_MAX;
		OP4_MIN; OP4_MUL; OP4_NE; OP4_OR; OP4_UDIV; OP4_UGE; OP4_ULT; OP4_UMAD; OP4_UMIN; OP4_UMAX; OP4_UMUL; OP4_YSHR; OP4_XOR;
		OP4_EXP; OP4_FRC; OP4_FTOI; OP4_FTOU; OP4_ITOF; OP4_LOG; OP4_MOV; OP4_MOVC; OP4_ROUND_NE; OP4_ROUND_NI; OP4_ROUND_PI;
		OP4_ROUND_Z; OP4_RSQ; OP4_SINCOS; OP4_SQRT; OP4_UTOF; OP4_DISCARD_Z; OP4_DISCARD_NZ; OP4_IF_NZ; OP4_IF_Z; OP4_LOOP;
		OP4_DCL; OP4_REGISTER_NULL; OP4_LITERAL_VALUE; OP4_SAMPLE; OP4_DERIVX; OP4_DERIVY;
		OP_MODIFIER; OP_REGISTER_MOD; OP_SWIZZLE; OP_INDEX;
		SM_VS_3_0; SM_PS_3_0; SM_VS_4_0; SM_PS_4_0; SM_VS_5_0; SM_PS_5_0; SM_VS_4_1; SM_PS_4_1;
	}
	
	@lexer::namespace{HLSL2GLSLLib}
	@parser::namespace{HLSL2GLSLLib}
	
	/* Parser Rules */
	
	public compileUnit
	  : sm=shaderModel { SetShaderModel($sm.tree.Token); } (definition*) declaration* instruction*  ( RET | EOF )
		-> ^(PROGRAM shaderModel definition* declaration* instruction*)
	  ;
	  
	definition
	  : DEF registerConstant (COMMA floatLiteral)* -> ^(OP_DEF registerConstant floatLiteral*)
	  | DEFI registerConstantInt (COMMA integerLiteral)* -> ^(OP_DEF registerConstantInt integerLiteral*)
	  | DEFB registerConstantBool COMMA booleanLiteral -> ^(OP_DEF registerConstantBool booleanLiteral)
	  ;
	  
	declaration
	  : {IsSM3}? op=DCL_POSITION (registerInput | registerOutput) -> ^(OP_DCL $op registerInput? registerOutput?)
	  | {IsSM3}? op=DCL_BLENDWEIGHT (registerInput | registerOutput) -> ^(OP_DCL $op registerInput? registerOutput?)
	  | {IsSM3}? op=DCL_BLENDINDICES (registerInput | registerOutput) -> ^(OP_DCL $op registerInput? registerOutput?)
	  | {IsSM3}? op=DCL_PSIZE (registerInput | registerOutput) -> ^(OP_DCL $op registerInput? registerOutput?)
	  | {IsSM3}? op=DCL_TANGENT (registerInput | registerOutput) -> ^(OP_DCL $op registerInput? registerOutput?)
	  | {IsSM3}? op=DCL_BINORMAL (registerInput | registerOutput) -> ^(OP_DCL $op registerInput? registerOutput?)
	  | {IsSM3}? op=DCL_COLOR (registerInput | registerOutput) -> ^(OP_DCL $op registerInput? registerOutput?)
	  | {IsSM3}? op=DCL_DEPTH (registerInput | registerOutput) -> ^(OP_DCL $op registerInput? registerOutput?)
	  | {IsSM3}? op=DCL_FOG (registerInput | registerOutput) -> ^(OP_DCL $op registerInput? registerOutput?)
	  | {IsSM3}? op=DCL_NORMAL (registerInput | registerOutput) -> ^(OP_DCL $op registerInput? registerOutput?)
	  | {IsSM3}? op=DCL_TEXCOORD (registerInput | registerOutput)-> ^(OP_DCL $op registerInput? registerOutput?)
	  | {IsSM3}? op=DCL_1D registerSampler -> ^(OP_DCL $op registerSampler)
	  | {IsSM3}? op=DCL_2D registerSampler -> ^(OP_DCL $op registerSampler)
	  | {IsSM3}? op=DCL_VOLUME registerSampler -> ^(OP_DCL $op registerSampler)
	  | {IsSM3}? op=DCL_CUBE registerSampler -> ^(OP_DCL $op registerSampler)
	  | {IsSM4}? DCL4_CONSTANTBUFFER -> ^(OP4_DCL) // TODO If Needed
	  | {IsSM4}? DCL4_IMMEDIATECONSTANTBUFFER LCURLY (LCURLY floatLiteral (COMMA floatLiteral)* RCURLY) (COMMA LCURLY floatLiteral (COMMA floatLiteral)* RCURLY)* RCURLY
		-> ^(OP4_DCL) // TODO If Needed
	  | {IsSM4}? DCL4_GLOBALFLAGS -> ^(OP4_DCL) // TODO If Needed
	  | {IsSM4}? DCL4_INDEXABLETEMP -> ^(OP4_DCL) // TODO If Needed
	  | {IsSM4}? DCL4_INPUT -> ^(OP4_DCL) // TODO If Needed
	  | {IsSM4}? DCL4_OUTPUT -> ^(OP4_DCL) // TODO If Needed
	  | {IsSM4}? DCL4_RESOURCE -> ^(OP4_DCL) // TODO If Needed
	  | {IsSM4}? DCL4_SAMPLER -> ^(OP4_DCL) // TODO If Needed
	  | {IsSM4}? DCL4_TEMPS -> ^(OP4_DCL) // TODO If Needed
	  ;
	  
	instruction
	  : binaryInstruction
	  | ternaryInstruction
	  | unaryInstruction
	  | {IsSM3}? sampleInstruction
	  | {IsSM4}? sample4Instruction
	  | ifInstruction
	  | {IsSM4}? switchInstruction // TODO
	  | loopInstruction
	  | breakInstruction
	  | {IsSM4}? continueInstruction
	  //| labelInstruction
	  | texkillInstruction
	  | lineDirective
	  | NOP
	  ;
	  
	lineDirective
	  : PREPROCESSOR_LINE integerLiteral stringLiteral? -> ^(OP_DEBUG_LINE integerLiteral stringLiteral?)
	  ;
	  
	instructionModifier
	  : MOD_SAT
	  ;
	  
	registerModifier
	  : MOD_ABS
	  ;
	  
	ternaryOperand
	  : {IsSM3}? CMP -> OP_CMP
	  | {IsSM3}? DP2ADD -> OP_DP2ADD
	  | {IsSM3}? LRP -> OP_LRP
	  | {IsSM3}? MAD -> OP_MAD
	  | {IsSM3}? SGN -> OP_SGN
	  | {IsSM4}? MAD -> OP4_MAD
	  | {IsSM4}? MOVC -> OP4_MOVC
	  | {IsSM4}? IMAD -> OP4_IMAD
	  | {IsSM4}? UMAD -> OP4_UMAD
	  ;
	  
	ternaryInstruction
	  : ternaryOperand instructionModifier? destRegister COMMA sourceRegister COMMA sourceRegister COMMA sourceRegister
		-> ^(ternaryOperand ^(OP_MODIFIER instructionModifier?) destRegister sourceRegister sourceRegister sourceRegister)
	  ;
	  
	binaryOperand
	  : {IsSM3}? ADD -> OP_ADD
	  | {IsSM3}? CRS -> OP_CRS
	  | {IsSM3}? DP3 -> OP_DP3
	  | {IsSM3}? DP4 -> OP_DP4
	  | {IsSM3}? DST -> OP_DST
	  | {IsSM3}? MAX -> OP_MAX
	  | {IsSM3}? MIN -> OP_MIN
	  | {IsSM3}? MUL -> OP_MUL
	  | {IsSM3}? POW -> OP_POW
	  | {IsSM3}? SGE -> OP_SGE
	  | {IsSM3}? SLT -> OP_SLT
	  | {IsSM3}? SUB -> OP_SUB
	  | {IsSM4}? ADD -> OP4_ADD
	  | {IsSM4}? AND -> OP4_AND
	  | {IsSM4}? DIV -> OP4_DIV
	  | {IsSM4}? DP2 -> OP4_DP2
	  | {IsSM4}? DP3 -> OP4_DP3
	  | {IsSM4}? DP4 -> OP4_DP4
	  | {IsSM4}? EQ -> OP4_EQ
	  | {IsSM4}? GE -> OP4_GE
	  | {IsSM4}? LT -> OP4_LT
	  | {IsSM4}? IADD -> OP4_IADD
	  | {IsSM4}? IEQ -> OP4_IEQ
	  | {IsSM4}? IGE -> OP4_IGE
	  | {IsSM4}? ILT -> OP4_ILT
	  | {IsSM4}? IMIN -> OP4_IMIN
	  | {IsSM4}? INE -> OP4_INE
	  | {IsSM4}? ISHL -> OP4_ISHL
	  | {IsSM4}? ISHR -> OP4_ISHR
	  | {IsSM4}? MAX -> OP4_MAX
	  | {IsSM4}? MIN -> OP4_MIN
	  | {IsSM4}? MUL -> OP4_MUL
	  | {IsSM4}? NE -> OP4_NE
	  | {IsSM4}? OR -> OP4_OR
	  | {IsSM4}? UDIV -> OP4_UDIV
	  | {IsSM4}? UGE -> OP4_UGE
	  | {IsSM4}? ULT -> OP4_ULT
	  | {IsSM4}? UMAD -> OP4_UMAD
	  | {IsSM4}? UMIN -> OP4_UMIN
	  | {IsSM4}? UMAX -> OP4_UMAX
	  | {IsSM4}? USHR -> OP4_YSHR
	  | {IsSM4}? XOR -> OP4_XOR
	  ;
	  
	binaryInstruction
	  : binaryOperand instructionModifier? destRegister COMMA sourceRegister COMMA sourceRegister
		-> ^(binaryOperand ^(OP_MODIFIER instructionModifier?) destRegister sourceRegister sourceRegister)
	  | {IsSM4}? IMUL instructionModifier? destRegister COMMA destRegister COMMA sourceRegister COMMA sourceRegister -> ^(OP4_IMUL ^(OP_MODIFIER instructionModifier?) destRegister destRegister sourceRegister sourceRegister)
	  | {IsSM4}? UMUL instructionModifier? destRegister COMMA destRegister COMMA sourceRegister COMMA sourceRegister -> ^(OP4_UMUL ^(OP_MODIFIER instructionModifier?) destRegister destRegister sourceRegister sourceRegister)
	  ;
	  
	unaryOperand
	  : {IsSM3}? ABS -> OP_ABS
	  | {IsSM3}? DSX -> OP_DSX
	  | {IsSM3}? DSY -> OP_DSY
	  | {IsSM3}? EXP -> OP_EXP
	  | {IsSM3}? FRC -> OP_FRC
	  | {IsSM3}? LOG -> OP_LOG
	  | {IsSM3}? MOV -> OP_MOV
	  | {IsSM3}? MOVA -> OP_MOVA
	  | {IsSM3}? NRM -> OP_NRM
	  | {IsSM3}? RCP -> OP_RCP
	  | {IsSM3}? RSQ -> OP_RSQ
	  | {IsSM3}? SINCOS -> OP_SINCOS
	  | {IsSM4}? DERIV_RTX -> OP4_DERIVX
	  | {IsSM4}? DERIV_RTY -> OP4_DERIVY
	  | {IsSM4}? EXP -> OP4_EXP
	  | {IsSM4}? FRC -> OP4_FRC
	  | {IsSM4}? FTOI -> OP4_FTOI
	  | {IsSM4}? FTOU -> OP4_FTOU
	  | {IsSM4}? ITOF -> OP4_ITOF
	  | {IsSM4}? LOG -> OP4_LOG
	  | {IsSM4}? MOV -> OP4_MOV
	  | {IsSM4}? ROUND_NE -> OP4_ROUND_NE
	  | {IsSM4}? ROUND_NI -> OP4_ROUND_NI
	  | {IsSM4}? ROUND_PI -> OP4_ROUND_PI
	  | {IsSM4}? ROUND_Z -> OP4_ROUND_Z
	  | {IsSM4}? RSQ -> OP4_RSQ
	  | {IsSM4}? SQRT -> OP4_SQRT
	  | {IsSM4}? UTOF -> OP4_UTOF
	  ;
	  
	unaryInstruction
	  : unaryOperand instructionModifier? destRegister COMMA sourceRegister -> ^(unaryOperand ^(OP_MODIFIER instructionModifier?) destRegister sourceRegister)
	  | {IsSM4}? SINCOS instructionModifier? d1=destRegister COMMA d2=destRegister COMMA sourceRegister -> ^(OP4_SINCOS ^(OP_MODIFIER instructionModifier?) $d1 $d2 sourceRegister)
	  ;
	  
	sampleInstruction
	  : TEXLD instructionModifier? destRegister COMMA sourceRegister COMMA registerSampler
		-> ^(OP_SAMPLE TEXLD ^(OP_MODIFIER instructionModifier?) destRegister sourceRegister registerSampler)
	  | TEXLDL instructionModifier? destRegister COMMA sourceRegister COMMA registerSampler
		-> ^(OP_SAMPLE TEXLDL ^(OP_MODIFIER instructionModifier?) destRegister sourceRegister registerSampler)
	  | TEXLDB instructionModifier? destRegister COMMA sourceRegister COMMA registerSampler
		-> ^(OP_SAMPLE TEXLDB ^(OP_MODIFIER instructionModifier?) destRegister sourceRegister registerSampler)
	  | TEXLDP instructionModifier? destRegister COMMA sourceRegister COMMA registerSampler
		-> ^(OP_SAMPLE TEXLDP ^(OP_MODIFIER instructionModifier?) destRegister sourceRegister registerSampler)
	  | TEXLDD instructionModifier? destRegister COMMA sourceRegister COMMA registerSampler COMMA x=sourceRegister COMMA y=sourceRegister
		-> ^(OP_SAMPLE TEXLDD ^(OP_MODIFIER instructionModifier?) destRegister sourceRegister registerSampler $x $y)
	  ;
	  
	sample4Instruction
	  : SAMPLE instructionModifier? destRegister COMMA sourceRegister COMMA registerTexture COMMA registerSampler
		-> ^(OP4_SAMPLE SAMPLE ^(OP_MODIFIER instructionModifier?) destRegister sourceRegister registerTexture registerSampler)
	  | SAMPLE_B instructionModifier? destRegister COMMA sourceRegister COMMA registerTexture COMMA registerSampler COMMA b=sourceRegister
		-> ^(OP4_SAMPLE SAMPLE_B ^(OP_MODIFIER instructionModifier?) destRegister sourceRegister registerTexture registerSampler $b)
	  | SAMPLE_C instructionModifier? destRegister COMMA sourceRegister COMMA registerTexture COMMA registerSampler COMMA b=sourceRegister
		-> ^(OP4_SAMPLE SAMPLE_C ^(OP_MODIFIER instructionModifier?) destRegister sourceRegister registerTexture registerSampler $b)
	  | SAMPLE_C_LZ instructionModifier? destRegister COMMA sourceRegister COMMA registerTexture COMMA registerSampler COMMA b=sourceRegister
		-> ^(OP4_SAMPLE SAMPLE_C_LZ ^(OP_MODIFIER instructionModifier?) destRegister sourceRegister registerTexture registerSampler $b)
	  | SAMPLE_D instructionModifier? destRegister COMMA sourceRegister COMMA registerTexture COMMA registerSampler COMMA x=sourceRegister COMMA y=sourceRegister
		-> ^(OP4_SAMPLE SAMPLE_D ^(OP_MODIFIER instructionModifier?) destRegister sourceRegister registerTexture registerSampler $x $y)
	  | SAMPLE_L instructionModifier? destRegister COMMA sourceRegister COMMA registerTexture COMMA registerSampler COMMA l=sourceRegister
		-> ^(OP4_SAMPLE SAMPLE_L ^(OP_MODIFIER instructionModifier?) destRegister sourceRegister registerTexture registerSampler $l)
	  ;
	  
	texkillInstruction
	  : {IsSM3}? TEXKILL sourceRegister -> ^(OP_TEXKILL sourceRegister)
	  | {IsSM4}? DISCARD_Z sourceRegister -> ^(OP4_DISCARD_Z sourceRegister)
	  | {IsSM4}? DISCARD_NZ sourceRegister -> ^(OP4_DISCARD_NZ sourceRegister)
	  ;
	  
	ifOperand : IF_GT | IF_LT | IF_GE | IF_LE | IF_EQ | IF_NE;
	
	ifInstruction
	  : {IsSM3}? ifOperand a=sourceRegister COMMA b=sourceRegister i+=instruction* (ELSE e+=instruction*)? ENDIF
		-> ^(OP_IF ifOperand $a $b ^(OP_IF_INSTR $i*) ^(OP_IF_ELSE_INSTR $e*))
	  | {IsSM3}? IF registerConstantBool i+=instruction* (ELSE e+=instruction*)? ENDIF
		-> ^(OP_IF IF registerConstantBool ^(OP_IF_INSTR $i*) ^(OP_IF_ELSE_INSTR $e*))
	  | {IsSM4}? IF_Z sourceRegister i+=instruction* (ELSE e+=instruction*)? ENDIF
		-> ^(OP4_IF_Z sourceRegister ^(OP_IF_INSTR $i*) ^(OP_IF_ELSE_INSTR $e*))
	  | {IsSM4}? IF_NZ sourceRegister i+=instruction* (ELSE e+=instruction*)? ENDIF
		-> ^(OP4_IF_NZ sourceRegister ^(OP_IF_INSTR $i*) ^(OP_IF_ELSE_INSTR $e*))
	  ;
	  
	switchInstruction
	  : SWITCH // TODO If Needed, unsure if SM4 uses the construct actively but have not seen it yet. Syntax seems a little sketchy too.
		-> ^(OP4_SWITCH)
	  ;
	  
	loopInstruction
	  : {IsSM3}? REP registerConstantInt i+=instruction* ENDREP
		-> ^(OP_REP registerConstantInt ^(OP_LOOP_INSTR $i*))
	  | {IsSM3}? LOOP registerAddress COMMA registerConstantInt i+=instruction* ENDLOOP
		-> ^(OP_REP registerAddress registerConstantInt ^(OP_LOOP_INSTR $i*))
	  | {IsSM4}? LOOP i+=instruction* ENDLOOP
		-> ^(OP4_LOOP $i*)
	  ;
	  
	breakOperand : BREAK_GT | BREAK_LT | BREAK_GE | BREAK_LE | BREAK_EQ | BREAK_NE;
	breakOperand4 : BREAKC_Z | BREAKC_NZ;
	
	breakInstruction
	  : {IsSM3}? BREAK -> OP_BREAK
	  | {IsSM3}? breakOperand a=sourceRegister COMMA b=sourceRegister -> ^(OP_BREAK breakOperand $a $b)
	  | {IsSM4}? BREAK -> OP4_BREAK
	  | {IsSM4}? breakOperand4 a=sourceRegister -> ^(OP4_BREAK breakOperand4 $a)
	  ;

	continueOperand : CONTINUEC_Z | CONTINUEC_NZ;

	continueInstruction
	  : CONTINUE -> OP4_CONTINUE
	  | continueOperand a=sourceRegister -> ^(OP4_CONTINUE continueOperand $a)
	  ;
	  
	labelInstruction
	  : CALL LABEL_TAG -> ^(OP_CALL LABEL_TAG)
	  | CALLNZ LABEL_TAG registerConstantBool -> ^(OP_CALL LABEL_TAG registerConstantBool)
	  | LABEL LABEL_TAG (i+=instruction)* -> ^(OP_LABEL LABEL_TAG $i)
	  // NOTE SM4: Not implemented, apparently not really used except for interfaces, implement if needed
	  ;
	  
	sourceRegister
	  : registerInput
	  | registerTemp
	  | registerConstant
	  | {IsSM4}? registerConstantBuffer
	  | {IsSM4}? registerImmediateConstantBuffer
	  | {IsSM4}? literalValue
	  ;
	  
	destRegister
	  : registerOutput
	  | registerTemp
	  | {IsSM3}? registerAddress
	  | {IsSM4}? registerNull
	  ;
	  
	registerInput
	  : MINUS? r=REGISTER_INPUT registerModifier? a=registerAddressing? (DOT s=SWIZZLE)?
		-> ^($r ^(OP_REGISTER_MOD MINUS? registerModifier?) ^(OP_SWIZZLE $s?)  ^(OP_INDEX $a?))
	  ;
	  
	registerOutput
	  : MINUS? r=REGISTER_OUTPUT a=registerAddressing? (DOT s=SWIZZLE)?
		-> ^($r ^(OP_REGISTER_MOD MINUS? ) ^(OP_SWIZZLE $s?) ^(OP_INDEX $a?))
	  ;
	  
	registerTemp
	  : MINUS? r=REGISTER_TEMP registerModifier? (DOT s=SWIZZLE)?
		-> ^($r ^(OP_REGISTER_MOD MINUS? registerModifier?) ^(OP_SWIZZLE $s?))
	  ;
	  
	registerConstant
	  : MINUS? r=REGISTER_CONSTANT registerModifier? a=registerAddressing? (DOT s=SWIZZLE)?
		-> ^($r ^(OP_REGISTER_MOD MINUS? registerModifier?) ^(OP_SWIZZLE $s?) ^(OP_INDEX $a?))
	  ;
	  
	registerConstantBuffer
	  : MINUS? r=REGISTER_CONSTANT_BUFFER registerModifier? a=registerAddressing? (DOT s=SWIZZLE)?
		-> ^($r ^(OP_REGISTER_MOD MINUS? registerModifier?) ^(OP_SWIZZLE $s?) ^(OP_INDEX $a?))
	  ;
	  
	registerImmediateConstantBuffer
	  : MINUS? r=REGISTER_IMMEDIATE_CONSTANT_BUFFER registerModifier? a=registerAddressing? (DOT s=SWIZZLE)?
		-> ^($r ^(OP_REGISTER_MOD MINUS? registerModifier?) ^(OP_SWIZZLE $s?) ^(OP_INDEX $a?))
	  ;
	  
	registerConstantInt
	  : MINUS? r=REGISTER_CONSTANT_INT registerModifier? a=registerAddressing? (DOT s=SWIZZLE)?
		-> ^($r ^(OP_REGISTER_MOD MINUS? registerModifier?) ^(OP_SWIZZLE $s?) ^(OP_INDEX $a?))
	  ;
	  
	registerConstantBool
	  : NOT? r=REGISTER_CONSTANT_BOOL a=registerAddressing?
		-> ^($r ^(OP_REGISTER_MOD NOT?) ^(OP_INDEX $a?))
	  ;
	  
	registerTexture
	  : MINUS? r=REGISTER_TEXTURE (DOT s=SWIZZLE)?
		-> ^($r ^(OP_REGISTER_MOD MINUS?) ^(OP_SWIZZLE $s?))
	  ;
	  
	registerAddress
	  : MINUS? r=REGISTER_ADDRESS (DOT s=SWIZZLE)?
		-> ^($r ^(OP_REGISTER_MOD MINUS?) ^(OP_SWIZZLE $s?))
	  ;
	  
	registerNull
	  : NULL -> OP4_REGISTER_NULL
	  ;
	  
	registerSampler
	  : MINUS? r=REGISTER_SAMPLER
		-> ^($r ^(OP_REGISTER_MOD MINUS?))
	  ;
	  
	registerAddressing
	  : LBRACKET registerAddressingExpression RBRACKET -> registerAddressingExpression
	  ;
	  
	registerAddressingExpression
	  :  (registerAddressingPrimary -> registerAddressingPrimary) (PLUS e=registerAddressingPrimary -> ^(OP_INDEX_PLUS $registerAddressingExpression $e))*
	  ;
	  
	registerAddressingPrimary
	  : integerLiteral
	  | {IsSM3}? registerAddress
	  | {IsSM4}? registerTemp
	  ;
	  
	shaderModel
	  : VS_4_0 -> SM_VS_4_0
	  | PS_4_0 -> SM_PS_4_0
	  | VS_3_0 -> SM_VS_3_0
	  | PS_3_0 -> SM_PS_3_0
	  | VS_4_1 -> SM_VS_4_1
	  | PS_4_1 -> SM_PS_4_1
	  | VS_5_0 -> SM_VS_5_0
	  | PS_5_0 -> SM_PS_5_0
	  ;
	  
	literalValue
	  : 'l' LPAREN f+=floatLiteral (COMMA f+=floatLiteral)* RPAREN -> ^(OP4_LITERAL_VALUE $f*)
	  ;
	  
	floatLiteral
	  : FLOAT_LITERAL
	  | DECIMAL_LITERAL
	  ;
	  
	integerLiteral
	  : DECIMAL_LITERAL
	  ;
	  
	booleanLiteral
	  : TRUE
	  | FALSE
	  ;
	  
	stringLiteral
	  : STRING_LITERAL
	  ;
	  
	/* ---------------------------------------------------------------------*/
	/* ---------------------------- Lexer Rules ----------------------------*/
	/* ---------------------------------------------------------------------*/
	
	NOT						: '!' ;
	LPAREN					: '(' ;
	RPAREN					: ')' ;
	LCURLY					: '{' ;
	RCURLY					: '}' ;
	PLUS					: '+' ;
	COMMA					: ',' ;
	MINUS					: '-' ;
	LBRACKET			    : '[' ;
	RBRACKET			    : ']' ;
	TRUE					: 'True';
	FALSE					: 'False';
	DOT						: '.' ;
	
	// instructions modifier----------------------------
	
	MOD_SAT					: '_sat';
	MOD_ABS					: '_abs';
	
	// instructions ----------------------------
	
	ABS						: 'abs';
	AND						: 'and';
	ADD						: 'add';
	BREAK					: 'break';
	BREAKC_Z				: 'breakc_z';
	BREAKC_NZ				: 'breakc_nz';
	BREAK_GT				: 'break_gt';
	BREAK_LT				: 'break_lt';
	BREAK_GE				: 'break_ge';
	BREAK_LE				: 'break_le';
	BREAK_EQ				: 'break_eq';
	BREAK_NE				: 'break_ne';
	CALL					: 'call';
	CALLNZ					: 'callnc';
	CMP						: 'cmp';
	CONTINUE				: 'continue';
	CONTINUEC_Z				: 'continuec_z';
	CONTINUEC_NZ			: 'continuec_nz';
	CRS						: 'crs';
	DEF						: 'def';
	DEFB					: 'defb';
	DEFI					: 'defi';
	DERIV_RTX				: 'deriv_rtx';
	DERIV_RTY				: 'deriv_rty';
	DISCARD_Z				: 'discard_z';
	DISCARD_NZ				: 'discard_nz';
	DIV						: 'div';
	DST						: 'dst';
	DSX						: 'dsx';
	DSY						: 'dsy';
	DP2						: 'dp2';
	DP2ADD					: 'dp2add';
	DP3						: 'dp3';
	DP4						: 'dp4';
	ELSE					: 'else';
	ENDIF					: 'endif';
	ENDLOOP					: 'endloop';
	ENDREP					: 'endrep';
	ENDSWITCH				: 'endswitch';
	EQ						: 'eq';
	EXP						: 'exp';
	FRC						: 'frc';
	FTOI					: 'ftoi';
	FTOU					: 'ftou';
	GE						: 'ge';
	IADD					: 'iadd';
	IEQ						: 'ieq';
	IF						: 'if';
	IF_GT					: 'if_gt';
	IF_LT					: 'if_lt';
	IF_GE					: 'if_ge';
	IF_LE					: 'if_le';
	IF_EQ					: 'if_eq';
	IF_NE					: 'if_ne';
	IF_NZ					: 'if_z';
	IF_Z					: 'if_nz';
	IGE						: 'ige';
	ILT						: 'ilt';
	IMAD					: 'imad';
	IMIN					: 'imin';
	IMUL					: 'imul';
	INE						: 'ine';
	INEG					: 'ineg';
	ISHL					: 'ishl';
	ISHR					: 'ishr';
	ITOF					: 'itof';
	LABEL					: 'label';
	LD						: 'ld';
	LOG						: 'log';
	LOOP					: 'loop';
	LRP						: 'lrp';
	LT						: 'lt';
	MAD						: 'mad';
	MAX						: 'max';
	MIN						: 'min';
	MOV						: 'mov';
	MOVA					: 'mova';
	MOVC					: 'movc';
	MUL						: 'mul';
	NE						: 'ne';
	NOP						: 'nop';
	NOT_FCT					: 'not';
	NRM						: 'nrm';
	NULL					: 'null';
	OR						: 'or';
	POW						: 'pow';
	RCP						: 'rcp';
	REP						: 'rep';
	RET						: 'ret';
	RETC_Z					: 'retc_z';
	RETC_NZ					: 'retc_nz';
	ROUND_NE				: 'round_ne';
	ROUND_NI				: 'round_ni';
	ROUND_PI				: 'round_pi';
	ROUND_Z					: 'round_z';
	RSQ						: 'rsq';
	SAMPLE					: 'sample';
	SAMPLE_B				: 'sample_b';
	SAMPLE_C				: 'sample_c';
	SAMPLE_C_LZ				: 'sample_c_lz';
	SAMPLE_D				: 'sample_d';
	SAMPLE_L				: 'sample_l';
	SGE						: 'sge';
	SGN						: 'sgn';
	SINCOS					: 'sincos';
	SLT						: 'slt';
	SQRT					: 'sqrt';
	SUB						: 'sub';
	SWITCH					: 'switch';
	TEXKILL					: 'texkill';
	TEXLD					: 'texld';
	TEXLDB					: 'texldb';
	TEXLDD					: 'texldd';
	TEXLDL					: 'texldl';
	TEXLDP					: 'texldp';
	UDIV					: 'udiv';
	UGE						: 'uge';
	ULT						: 'ult';
	UMAD					: 'umad';
	UMAX					: 'umax';
	UMIN					: 'umin';
	UMUL					: 'umul';
	USHR					: 'ushr';
	UTOF					: 'utof';
	XOR						: 'xor';
	
	// keywords ----------------------------
	
	PS_4_0					: 'ps_4_0';
	VS_4_0					: 'vs_4_0';
	PS_4_1					: 'ps_4_1';
	VS_4_1					: 'vs_4_1';
	PS_5_0					: 'ps_5_0';
	VS_5_0					: 'vs_5_0';
	PS_3_0					: 'ps_3_0';
	VS_3_0					: 'vs_3_0';
	
	/* ------------------------ Fundalental Tokens ------------------------*/
	
	fragment EXPONENT : ('e'|'E') (PLUS | MINUS)? ('0'..'9')+ ;
	
	DECIMAL_LITERAL
	  :     ('0'..'9')+
	  ;
	  
	FLOAT_LITERAL
	  : (PLUS | MINUS)?  DECIMAL_LITERAL '.' ('0'..'9')* (EXPONENT)?
	  | (PLUS | MINUS)?  '.' DECIMAL_LITERAL (EXPONENT)?
	  | (PLUS | MINUS)?  DECIMAL_LITERAL (EXPONENT)?
	  ;
	  
	DCL_POSITION : 'dcl_position' DECIMAL_LITERAL?;
	DCL_BLENDWEIGHT : 'dcl_blendweight' DECIMAL_LITERAL?;
	DCL_BLENDINDICES : 'dcl_blendindices' DECIMAL_LITERAL?;
	DCL_PSIZE : 'dcl_psize' DECIMAL_LITERAL?;
	DCL_TANGENT : 'dcl_tangent' DECIMAL_LITERAL?;
	DCL_BINORMAL : 'dcl_binormal' DECIMAL_LITERAL?;
	DCL_COLOR : 'dcl_color' DECIMAL_LITERAL?;
	DCL_FOG : 'dcl_fog' DECIMAL_LITERAL?;
	DCL_DEPTH : 'dcl_depth' DECIMAL_LITERAL?;
	DCL_NORMAL : 'dcl_normal' DECIMAL_LITERAL?;
	DCL_TEXCOORD : 'dcl_texcoord' DECIMAL_LITERAL?;
	DCL_1D : 'dcl_1d' DECIMAL_LITERAL?;
	DCL_2D : 'dcl_2d' DECIMAL_LITERAL?;
	DCL_VOLUME : 'dcl_volume' DECIMAL_LITERAL?;
	DCL_CUBE : 'dcl_cube' DECIMAL_LITERAL?;
	
	// SM4-5 Decls
	DCL4_CONSTANTBUFFER : 'dcl_constantbuffer' (~('\n'|'\r'))*;
	DCL4_GLOBALFLAGS : 'dcl_globalflags'  (~('\n'|'\r'))*;
	DCL4_IMMEDIATECONSTANTBUFFER : 'dcl_immediateConstantBuffer';
	DCL4_INDEXABLETEMP : 'dcl_indexabletemp' (~('\n'|'\r'))*;
	DCL4_INPUT : 'dcl_input' (~('\n'|'\r'))*;
	DCL4_OUTPUT : 'dcl_output' (~('\n'|'\r'))*;
	DCL4_RESOURCE : 'dcl_resource' (~('\n'|'\r'))*;
	DCL4_SAMPLER : 'dcl_sampler' (~('\n'|'\r'))*;
	DCL4_TEMPS : 'dcl_temps' (~('\n'|'\r'))*;
	
	REGISTER_INPUT : 'v' DECIMAL_LITERAL?;
	REGISTER_TEMP : 'r' DECIMAL_LITERAL;
	REGISTER_CONSTANT : 'c' DECIMAL_LITERAL?;
	REGISTER_CONSTANT_BUFFER : 'cb' DECIMAL_LITERAL?;
	REGISTER_IMMEDIATE_CONSTANT_BUFFER : 'icb' DECIMAL_LITERAL?;
	REGISTER_CONSTANT_INT : 'i' DECIMAL_LITERAL?;
	REGISTER_CONSTANT_BOOL : 'b' DECIMAL_LITERAL?;
	REGISTER_SAMPLER : 's' DECIMAL_LITERAL;
	REGISTER_TEXTURE : 't' DECIMAL_LITERAL;
	REGISTER_OUTPUT : ('o' | 'oC' | 'oDepth') DECIMAL_LITERAL?;
	REGISTER_ADDRESS : ('a' DECIMAL_LITERAL) | 'aL';
	
	LABEL_TAG : 'l' DECIMAL_LITERAL?;
	
	SWIZZLE : ('x' | 'y' | 'z' | 'w')+;
	
	STRING_LITERAL
	  :  '"' ( ~'"' )* '"'
	  ;
	  
	PREPROCESSOR_LINE : '#line';
	
	WHITESPACE : ( '\t' | ' ' | '\r' | '\n'| '\u000C' )+ 	{ $channel = Hidden; } ;
	COMMENT : '//' (~('\n'|'\r'))* { $channel = Hidden; } ;
	MULTILINE_COMMENT : '/*' ( options {greedy=false;} : . )* '*/' { $channel = Hidden; } ;
	//PREPROCESSOR : '#' (~('\n'|'\r'))* { $channel = Hidden; } ;